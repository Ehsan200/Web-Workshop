مبانی کامپوننت ها:

کامپوننت ها به ما این امکان را می دهند که رابط کاربری را به قسمت های مستقل و قابل استفاده تقسیم کنیم و در مورد هر قطعه به صورت مجزا فکر کنیم. رایج است که یک برنامه دارای اجزای درختی تو در تو باشد.
این بسیار شبیه به نحوه قرار دادن المنت های اصلی HTML است، اما Vue مدل کامپوننت های خود را طوری پیاده‌سازی می‌کند که به ما امکان می‌دهد محتوا و منطق موردنظر را در هر مؤلفه کپسوله کنیم. Vue همچنین کامپوننت های وب اصلی را به خوبی پیاده می کند.

تعریف کردن کامپوننت:

 هنگام استفاده از دستور build، ما معمولاً هر مؤلفه Vue را در یک فایل اختصاصی با استفاده از پسوند .vue تعریف می کنیم - که به عنوان یک مؤلفه تک فایل (به اختصار SFC) شناخته می شود:
```html
<script>
export default {
  data() {
    return {
      count: 0
    }
  }
}
</script>

<template>
  <button @click="count++">You clicked me {{ count }} times.</button>
</template>
```


استفاده از کامپوننت # 
نکته : ما از دستور SFC در ادامه مطلب استفاده خواهیم کرد - مفاهیم پیرامون کامپوننت ها بدون توجه به اینکه از دستور buils استفاده می کنید یا نه یکسان هستند. بخش Examples استفاده از کامپوننت را در هر دو سناریو نشان می دهد.

برای استفاده از کامپوننت فرزند، باید آن را در مولفه والد ایمپورت کنیم. با فرض اینکه کامپوننت شمارنده خود را در فایلی به نام ButtonCounter.vue قرار داده ایم، کامپوننت به علت اکسپورت پیش فرض انجام شده در فایل در معرض نمایش قرار می گیرد:
```html
<script>
import ButtonCounter from './ButtonCounter.vue'

export default {
  components: {
    ButtonCounter
  }
}
</script>

<template>
  <h1>Here is a child component!</h1>
  <ButtonCounter />
</template>
```

پاس دادن پروپرتی ها :

اگر در حال ساختن یک بلاگ هستیم، احتمالاً به مؤلفه ای نیاز خواهیم داشت که نشان دهنده یک پست وبلاگ باشد. ما می خواهیم همه پست های وبلاگ طرح بصری یکسانی داشته باشند، اما با محتوای متفاوت. چنین مؤلفه ای مفید نخواهد بود مگر اینکه بتوانید داده هایی مانند عنوان و محتوای پست خاصی را که می خواهیم نمایش دهیم به آن منتقل کنید. اینجاست که props وارد می شوند. Props ویژگی های سفارشی هستند که می توانید روی یک المنت ثبت کنید. برای پاس دادن عنوان به مؤلفه پست وبلاگ خود، باید آن را در لیست مواردی که این مؤلفه می پذیرد، با استفاده از گزینه props اعلام کنیم:

```html
<!-- BlogPost.vue -->
<script>
export default {
  props: ['title']
}
</script>

<template>
  <h4>{{ title }}</h4>
</template>
```


گوش دادن به رویدادها (event listening):

 همانطور که ما جزء <BlogPost> خود را توسعه می دهیم، ممکن است برخی از فیچر ها نیاز به برقراری ارتباط با والدین داشته باشند. به عنوان مثال، ممکن است تصمیم بگیریم یک فیچر دسترسی را برای بزرگ‌نمایی متن پست‌های وبلاگ در نظر بگیریم، در حالی که بقیه صفحه را در اندازه پیش‌فرض باقی می‌گذاریم. در والد، می‌توانیم با افزودن ویژگی داده postFontSize از این ویژگی پشتیبانی کنیم:

  ```js
  data() {
  return {
    posts: [
      /* ... */
    ],
    postFontSize: 1
  }
}
  ```

توزیع محتوا با slot :
  
 درست مانند عناصر HTML، اغلب مفید است که بتوانیم محتوا را به یک مؤلفه منتقل کنیم، مانند این:
```html
<AlertBox>
  Something bad happened.
</AlertBox>
```

که ممکن است چیزی شبیه به:
" این یک خطا برای اهداف نمایشی است" رندر شود. این را می توان با استفاده از عنصر سفارشی <slot> بدست آورد:
```html
<template>
  <div class="alert-box">
    <strong>This is an Error for Demo Purposes</strong>
    <slot />
  </div>
</template>

<style scoped>
.alert-box {
  /* ... */
}
</style>
```


محدودیت های قرار دادن عنصر :
  
برخی از عناصر HTML  محدودیت هایی در مورد اینکه چه عناصری می توانند در داخل آنها ظاهر شوند دارند و برخی از عناصر مانند option فقط می توانند در داخل برخی از عناصر دیگر ظاهر می شود. این منجر به مشکلاتی در هنگام استفاده از مؤلفه هایی با عناصری می شود که چنین محدودیت هایی دارند. مثلا:
```html
<table>
  <blog-post-row></blog-post-row>
</table>
```
  
کامپوننت سفارشی <blog-post-row> به عنوان محتوای نامعتبر برجسته می شود و باعث ایجاد خطا در خروجی رندر شده نهایی می شود. می توانیم از ویژگی special is به عنوان راه حل استفاده کنیم:
```html
<table>
  <tr is="vue:blog-post-row"></tr>
</table>
```

