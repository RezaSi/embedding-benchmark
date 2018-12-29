<div dir='rtl'>
  
  <p> 
  <b>
  راهنمای فایل farsnet-semantic-similarity-dataset.csv
    </b>
  
این فایل comma-separated می باشد و مشتمل بر 14 ستون است به ترتیب زیر:
  
  | 1  | 2| 3| 4| 5| 6| 7| 8| 9| 10| 11| 12 | 13 | 14 |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
|Word 1   | Word 2  |FarsnetSim1 | FarsnetSim2 | wup | jcn | vector | vector-pairwise | res | lin | path | lch | hso | lesk|
  
<p> 
  <b>
روش path
    </b>

این الگوریتم، ارتباط معنایی یا شباهت دو مجموعه ترادف را با شمارش تعداد گره ها موجود در کوتاه ترین مسیر موجود در فارس نت محاسبه می کند. طول مسیرهاشامل گره پایانی نیز می شود. is-a میان آن دو در سلسله مراتب
ازآنجاکه مسیر طولانی ترنشان دهنده ارتباط معنایی کمتر است، عدد خروجی که نشان دهنده میزان شباهت است معکوس طول کوتاه ترین مسیر بین دو مفهوم است که مطابق زیر محاسبه می شود:

<img src="http://latex.codecogs.com/gif.latex?relatedness%3D%5Cfrac%7B1%7D%7Bdistance%7D"><img/>


چنانچه دو مفهوم یکی باشند، فاصله آن دو یک خواهد بود پس شباهت نیز یک خواهد شد.


چنانچه مسیري بین دو مفهوم وجود نداشته باشد آنگاه مقدار 2-بازگردانده خواهد شد. براي محاسبه کوتاه ترین
مسیر در این روش فقط روابط is-a استفاده شده اند همچنین رابطه ها بدون جهت در نظر گرفته شدند.

</p> 


<p> 
  <b>
روش Wup
    </b>
  
الگوریتم ارائه شده توسط Wu & Palmer که براساس شمارش گره هاست در این پیمانه پیاده سازي شده است. در این روش شباهت براساس عمق دو مجموعه ترادف در سلسله مراتب و همچنین عمق گره LCS آن دو محاسبه می شود.
بدین ترتیب مقدار شباهت همواره به صورت
  <img src="http://latex.codecogs.com/gif.latex?0%3C%20score%5Cleq%201"><img/> است.


ازآنجاکه عمق lcs هرگز صفر نیست (عمق ریشه سلسله مراتب یک است) پس هیچ گاه شباهت صفر نخواهد شد. و اگر دو مجموعه ترادف یکی باشند آنگاه مقدار شباهت یک خواهد شد.

lcs دو گره، عمیق ترین گره در سلسله مراتب است که نیاي هر دو نیز باشد.
</p> 

<p> 
  <b>
روش lch
    </b>
  
الگوریتم ارائه شده توسط Leacock and Chodorow که شباهت دو مجموعه ترادف و یا دو نمود را به صورت زیر محاسبه می کند. این روش تعداد یال ها بین دو گره را در سلسله مراتب is-a فارس نت شمارش می کند. سپس عدد به دست آمده را با استفاده از بیشینه عمق در سلسله مراتب is-a  فارس نت مقیاس می نماید. درنهایت میزان شباهت، منفی لگاریتم عدد به دست آمده خواهد بود.

اگر مسیري بین دو مفهوم وجود نداشته باشد 2- بازگردانده می شود.

بیشینه عمق سلسله مراتببراساس نسخه مورداستفاده از فارس نت ممکن است متغیر باشد ولی مقدار 21 برای ریشه یکتاي سلسله مراتب is-a در نسخه فعلی فارس نت است.

</p> 

<p> 
  <b>
روش lesk
    </b>
  
این الگوریتم براساس کار Banerjee and Pedersen از اشتراکات معنی ها (gloss) هر مفهوم استفاده می کند. این روش مطابق با ویژگی ها موجود در فارس نت پیاده سازي شده است. در این الگوریتم از فارس نت به عنوان یک واژه نامه براي دسترسی به معنی هر واژه استفاده می شود.

بدین ترتیب براي هر دو مفهوم موردنظر، اشتراکات gloss براي خود واژه و مفاهیم پدر و فرزند آن دو محاسبه می شود.
براي محاسبه مقدار اشتراکات براي هر دو جمله از روش زیر استفاده می شود.

ابتدا همه ایست واژه ها حذف شدهو تک تک واژه ها ریشه یابیمی شوند. سپس در هر تکرار طولانی ترین زیرمجموعه مشترك واژه ها استخراج می گردد. امتیاز هر اشتراك در هر مرحله، مربع طول زیرمجموعه مشترك در آن مرحله است. و درنهایت امتیاز همه مراحل باهم جمع خواهد شد.
خروجی نهایی، مجموع امتیاز حاصل از اشتراکات معانی است که در بالا اشاره شد.

</p> 



<p> 
  <b>
روش VectorGloss
    </b>
  
در این روش شباهت مجموعه هاي ترادف با استفاده از بردار هم وقوعی مرتبه دوم معنی (gloss) هریک محاسبه می شود.


بردار هم وقوعی مرتبه دوم یا بردار زمینه (context vector) را Schütze در سال 1998 معرفی کرد.
Pedersen وPatwardhan از این بردارها براي بازنمایی نمود واژه ها استفاده کردند.
این الگوریتم با استفاده از روش Pedersen وPatwardhan پیاده سازي شده است. بردارهاهم وقوعی مرتبه دوم با استفاده از واژه نامه متشکل از معناهاي (gloss) موجود در فارس نت محاسبه شده اند.


درنهایت براي محاسبه شباهت دو مجموعه ترادف، کسینوس بردارها زمینه متناظر با آن دو محاسبه شده و بازگردانده می شود. علاوه بر معناهاي (gloss) خود مفاهیم، از معناهاي (gloss)  مفاهیم داراي رابطه با مفهوم مورد نظر نیز براي محاسبه این معیار شباهت استفاده می شود.


بدین ترتیب با ترکیب معناهاي (gloss)  همه مفاهیم داراي رابطه با مفهوم مورد نظر، یک معناي واحد طولانی وکامل (super gloss) ساخته می شود. درنهایت بردارهاي زمینه متناظر با این معناي جدید ساخته شده و شباهت محاسبه می شود. مقدار این شباهت می تواندبزرگ تر و یا برابر صفر باشد.


</p> 

<p> 
  <b>
روش Gloss vector (pairwise)
    </b>
  

در فارس نت همان طور که هر مفهوم بامعنی (gloss) خود معرفی می شود، معنی مفاهیم همسایه آن نیز در بازنمایی کامل تر معنا و جایگاه آن مفهوم نقش دارند.


با جایگزینی تک تک واژه ها هر معنی (gloss)  با بردارهاي هم وقوعی آنها، کل معنا به بردار مرتبه دوم تبدیل می گردد. با این کار به جاي هرمعنا (gloss)  یک بردار مرتبه دو داریم. شباهت نهایی دو مفهوم با محاسبه کسینوس دوبه دوي بردارهاي توسعه یافته به دست می آید. روابط مورداستفاده در این روش شامل همه رابطه هاي تعریف شده در فارس نت می باشد.


به بیان دیگر تفاوت این روش با روش vector در این است که در اینجا بردارهاي مجزا به ازاي هر یک از مفاهیم داراي رابطه با مفهوم مورد نظر ساخته می شود. به عنوان مثال بردارهاي جداگانه براي hypernym و hyponym و به همین ترتیب براي سایر روابط هر دو مفهوم ساخته می شود. در نهایت شباهت بردارهاي متناظر، محاسبه شده و مجموع این شباهت ها به عنوان معیار نهایی در نظر گرفته می شود. در واقع شباهت بردارهاي hypernym دو مفهوم و شباهت بردارهاي hyponym دو مفهوم و ... با هم جمع شده و مقدار نهایی محاسبه می گردد.

</p> 




<p> 
  <b>
روش lin
    </b>
  

Lin در سال 1998 روشی براي محاسبه ارتباط معنایی نمود واژه ها معرفی نمود که ازاطلاعات محتوایی مفاهیم (information content) در وردنت و نظریه شباهت (Similarity Theorem) استفاده می کند.

در این روش شباهت دو مفهوم با استفاده از فرمول زیر محاسبه می شود. که مقدار آن عددي کوچک تر یا مساوي یک و بزرگ تر یا مساوي 0 خواهد بود.


مقدار شباهت برابر است با دوبرابر اطلاعات محتوایی lcs دو مفهوم تقسیم بر مجموع اطلاعات محتوایی آن دو.
براي محاسبه اطلاعات محتوایی، چند روش مختلف معرفی شده اند که در اینجا از روش زیر استفاده شده است.
اطلاعات محتوایی مفهوم c برابر است با نسبت تعداد برگ هاي که در سلسله مراتب که زیر مفهوم c قرار دارند به تعداد مفاهیمی که نیاي مفهوم c هستند. و درنهایت این مقدار با استفاده از اطلاعات محتوایی مفهوم ریشه که داراي کمترین اطلاعات محتوایی است نرمال می شود. این مقدار برابر با تعداد همه برگ هاسلسله مراتب است.


</p> 


<p> 
  <b>
روش res
    </b>
  
این روش نیز مبتنی بر اطلاعات محتوایی دو مفهوم است. محاسبه شباهت دو مفهوم به این روش توسط Resnik 	در سال 1995 مطرح شد. وي شباهت دو مفهوم را برابر با اطلاعات محتوایی lcs آن دو مطرح کرد. که مقدار آن بین 0 و یک خواهد بود.
</p> 


<p> 
  <b>
روش hso
    </b>
  
St-Onge وHirst  در سال 1998 براي محاسبه شباهت دو مفهوم روشی را ارائه کردند. در این روش، ارتباط معنایی دو مجموعه ترادف با استفاده از یافتن زنجیره های واژگانی ('lexical chains) معرفی شده توسط آنها محاسبه می شود.

این الگوریتم از کوتاه ترینمسیر بین دو مفهوم استفاده می کند. اما مسیرهافقط از روابط سلسله مراتبی تشکیل نشده اند. همه انواع رابطه ها مجاز شمرده می شوند. به طورخلاصه در این روش به هریک از انواع رابطه ها موجود در فارس نت جهت هاي داده می شود. سپس کوتاه ترین مسیر بین دو مفهوم که داراي کمترین تغییر جهت باشد، تعیین می گردد.
</p> 
<hr />


<p> 
  <b>
منابع
    </b>

<ul>
  <li>http://farsnet.nlp.sbu.ac.ir</li>
    
  </ul>
  </p>

</div>
