<div dir = "rtl">
<h1 dir = "rtl">
رندر کردن شرطی:
</h1>

<h2>
دستور v-if:
</h2>

دستور v-if برای رندر کردن یک بلوک به صورت مشروط استفاده می شود. بلوک تنها در صورتی ارائه می شود که عبارت دستور یک مقدار واقعی را برگرداند.

```vue
<h1 v-if="awesome">Vue is awesome!</h1>
```
<h2>
دستور v-else:
</h2>

می‌توانید از دستور v-else برای نشان دادن یک بلوک else برای v-if استفاده کنید:

```vue
<button @click="awesome = !awesome">Toggle</button>
```
```vue
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```
<h2>
دستور v-else-if:
</h2>
v-else-if، همانطور که از نام آن پیداست، به عنوان یک شرط جدید در صورت نقض شرط برای v-if عمل می کند. همچنین می توان آن را چندین بار زنجیر کرد:

```vue
<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>	
```
<h2>
دستور v-show:
</h2>
گزینه دیگر برای نمایش شرطی یک عنصر دستور v-show است. کاربرد تا حد زیادی یکسان است:

```vue
<h1 v-show="ok">Hello!</h1>
```

تفاوت این است که یک عنصر با v-show همیشه رندر می شود و در DOM باقی می ماند. v-show فقط ویژگی نمایش CSS عنصر را تغییر می دهد.

<h3>
مقایسه v-if  با v-show :
</h3>
v-if رندر شرطی «واقعی» است زیرا تضمین می‌کند که لیسنرهای رویداد و مؤلفه‌های فرزند در داخل بلوک شرطی به درستی از بین رفته و در حین جابجایی دوباره ایجاد می‌شوند. v-if نیز به صورت lazy است: اگر شرط در رندر اولیه false باشد، کاری انجام نمی دهد - بلوک شرطی تا زمانی که شرط برای اولین بار درست نشود، رندر نمی شود. در مقایسه، v-show بسیار ساده‌تر است - عنصر همیشه بدون در نظر گرفتن شرایط اولیه، با جابجایی مبتنی بر CSS ارائه می‌شود. به طور کلی، v-if دارای هزینه های تعویض بالاتر است در حالی که v-show هزینه های رندر اولیه بالاتری دارد. بنابراین اگر نیاز دارید چیزی را اغلب تغییر دهید v-show را ترجیح دهید و اگر بعید است که شرایط در زمان اجرا تغییر کند، v-if را ترجیح دهید.

</div>