<!DOCTYPE html>
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تشخیص چهره با PCA و Eigenfaces</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            color: #333;
        }
        header {
            background-color: #4CAF50;
            color: white;
            padding: 10px 0;
            text-align: center;
        }
        h1, h2 {
            font-size: 2em;
            color: #4CAF50;
        }
        .content {
            margin: 20px;
        }
        .section {
            background-color: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }
        .section h2 {
            font-size: 1.5em;
            color: #333;
        }
        .section p {
            font-size: 1.1em;
            color: #666;
        }
        .highlight {
            background-color: #f9f9f9;
            padding: 10px;
            border-left: 5px solid #4CAF50;
            margin: 20px 0;
        }
        .models, .results {
            background-color: #fafafa;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
        }
        .models ul, .results ul {
            list-style-type: none;
            padding: 0;
        }
        .models li, .results li {
            background-color: #eee;
            padding: 10px;
            margin: 5px 0;
            border-radius: 5px;
        }
    </style>
</head>
<body>

    <header>
        <h1>تشخیص چهره با استفاده از PCA و Eigenfaces</h1>
    </header>

    <div class="content">
        <div class="section">
            <h2>توضیح پروژه</h2>
            <p>
                این پروژه به بررسی <strong>تشخیص چهره</strong> با استفاده از تکنیک <strong>Eigenfaces</strong> (بر اساس الگوریتم <strong>PCA</strong> برای کاهش ابعاد) پرداخته است. دیتاست استفاده شده، <strong>Olivetti Faces</strong>، شامل <strong>۴۰۰ تصویر سیاه‌وسفید</strong> از ۴۰ نفر مختلف است (هر نفر ۱۰ تصویر با تغییرات نور، حالت چهره و زاویه).
            </p>
        </div>

        <div class="section">
            <h2>دیتاست: Olivetti Faces</h2>
            <p>
                <strong>دیتاست Olivetti Faces</strong> یک مجموعه استاندارد برای آزمایش الگوریتم‌های تشخیص چهره است که شامل <strong>تصاویر ۶۴x۶۴ پیکسلی</strong> می‌باشد و به <strong>وکتورهای ۴۰۹۶ بعدی</strong> تبدیل می‌شود. از <strong>PCA</strong> برای استخراج <strong>Eigenfaces</strong> (چهره‌های اصلی) استفاده می‌شود تا داده‌ها به فضای کم‌بعدی‌تری پروژه شوند و نویز کاهش یابد.
            </p>
        </div>

        <div class="section">
            <h2>روش‌شناسی: گام به گام</h2>
            <div class="highlight">
                <p>
                    این پروژه شامل مراحل زیر است:
                </p>
                <ul>
                    <li><strong>اعمال PCA:</strong> ابتدا از PCA برای استخراج کامپوننت‌های اصلی (Eigenfaces) استفاده می‌شود.</li>
                    <li><strong>بازسازی تصاویر:</strong> تصاویر بازسازی شده برای ارزیابی کیفیت کاهش ابعاد نمایش داده می‌شوند.</li>
                    <li><strong>تقسیم داده‌ها:</strong> داده‌ها به دو بخش <strong>آموزشی (۸۰%)</strong> و <strong>آزمایشی (۲۰%)</strong> تقسیم می‌شوند.</li>
                    <li><strong>مقایسه مدل‌ها:</strong> مدل‌های مختلف طبقه‌بندی آموزش می‌بینند و این فرآیند برای هر تعداد کامپوننت تکرار می‌شود.</li>
                </ul>
            </div>
        </div>

        <div class="models">
            <h2>مدل‌های مقایسه‌شده</h2>
            <ul>
                <li><strong>SVM (Linear/RBF):</strong> مدل‌های کرنلی، هم خطی و هم غیرخطی، در وظایف تشخیص چهره با ویژگی‌های استخراج شده از PCA عملکرد بسیار خوبی دارند.</li>
                <li><strong>Random Forest:</strong> یک آنسامبل از درخت‌های تصمیم برای مدیریت پیچیدگی داده‌ها و جلوگیری از <strong>overfitting</strong>.</li>
                <li><strong>AdaBoost:</strong> تکنیک <strong>boosting</strong> برای تقویت مدل‌های ضعیف. اما در اینجا عملکرد کمتری نشان می‌دهد که ممکن است به دلیل حساسیت به نویز در داده‌های چهره باشد.</li>
            </ul>
        </div>

        <div class="results">
            <h2>نتایج و اهمیت</h2>
            <p>
                این پروژه اهمیت <strong>PCA</strong> را در کاهش بار محاسباتی (از <strong>۴۰۹۶ ویژگی به ۱۰</strong>) نشان می‌دهد و در عین حال بهبود عملکرد مدل‌ها را نیز بیان می‌کند. مدل‌های <strong>SVM</strong> با تعداد بیشتر کامپوننت‌ها به دقت بالای <strong>۸۰%</strong> می‌رسند، در حالی که <strong>AdaBoost</strong> به صورت استاتیک باقی می‌ماند.
            </p>
        </div>
    </div>

</body>
</html>
