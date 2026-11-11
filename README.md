

# Logs
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*
lerna-debug.log*

node_modules
dist
dist-ssr
*.local

# Editor directories and files
.vscode/*
!.vscode/extensions.json
.idea
.DS_Store
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?

# Vercel
.vercel
.env
.env.local

# =========================================================================
# إعدادات خوادم Apache / cPanel / LiteSpeed لنظام المخازن ونقاط البيع (MCC Sale)
# يدعم إعادة توجيه المسارات الكاملة (SPA Rewrites) بدون ظهور صفحة 404
# متوافق مع الدومين: https://mccsale.vercel.app وأي دومين مخصص (Custom Domain)
# =========================================================================

<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /

  # السماح بالوصول المباشر للملفات والمجلدات الحقيقية
  RewriteRule ^index.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteCond %{REQUEST_FILENAME} !-l

  # إعادة توجيه كافة المسارات وشاشات الكاشير إلى صفحة index.html
  RewriteRule . /index.html [L]
</IfModule>

# ترويسات الأمان والتوافق مع الحافظة (Clipboard) للنسخ على كروم وأوبرا
<IfModule mod_headers.c>
  Header set X-Content-Type-Options "nosniff"
  Header set X-Frame-Options "SAMEORIGIN"
  Header set Access-Control-Allow-Origin "*"
  Header set Permissions-Policy "clipboard-write=(self), clipboard-read=(self)"
</IfModule>

# ضغط الملفات Gzip / Deflate لسرعة استجابة فائقة
<IfModule mod_deflate.c>
  AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css text/javascript application/javascript application/json application/xml
</IfModule>

# تعريف أنواع الوسائط بدقة (MIME Types)
<IfModule mod_mime.c>
  AddType text/javascript .js
  AddType text/css .css
  AddType application/json .json
  AddType application/vnd.ms-access .accdb
</IfModule>

/*    /index.html   200

<!doctype html>
<html lang="ar" dir="rtl">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>نظام المخازن والمبيعات ونقاط البيع | MCC Sale</title>
    <meta name="description" content="نظام نقاط البيع والمخازن المتكامل مع الربط الإلكتروني لهيئة الزكاة والضريبة والجمارك (ZATCA Phase 2) وإدارة المبيعات ونقاط البيع للكاشير. دومين mccsale.vercel.app" />
    <link rel="canonical" href="https://mccsale.vercel.app" />
    
    <!-- Open Graph & Social Cards -->
    <meta property="og:title" content="نظام المخازن والمبيعات المتكامل - MCC Sale" />
    <meta property="og:description" content="برنامج نقاط البيع والمخازن والفاتورة الإلكترونية مع رابط الكاشير السريع ودعم دومين mccsale.vercel.app" />
    <meta property="og:type" content="website" />
    <meta property="og:url" content="https://mccsale.vercel.app" />
    <meta name="twitter:card" content="summary_large_image" />
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;500;600;700;800;900&family=Tajawal:wght@400;500;700&display=swap" rel="stylesheet" />
    
    <style>
      @media print {
        body {
          background: white !important;
          color: black !important;
        }
        .no-print {
          display: none !important;
        }
        .print-only {
          display: block !important;
        }
      }
      @media screen {
        .print-only {
          display: none !important;
        }
      }
    </style>
  </head>
  <body class="bg-slate-50 text-slate-900 antialiased font-['Cairo',sans-serif] selection:bg-blue-600 selection:text-white">
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>

# =========================================================================
# إعدادات Nginx Server Block لاستضافة نظام المخازن والمبيعات (MCC Sale)
# =========================================================================
server {
    listen 80;
    server_name mccsale.vercel.app yourdomain.com;
    root /var/www/mccsale;
    index index.html;

    # Gzip Compression
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml image/svg+xml;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location /assets/ {
        expires 1y;
        add_header Cache-Control "public, no-transform";
    }

    add_header X-Content-Type-Options "nosniff";
    add_header X-Frame-Options "SAMEORIGIN";
    add_header Access-Control-Allow-Origin "*";
}

{
  "name": "mccsale-pos-system",
  "private": true,
  "version": "1.0.0",
  "description": "نظام المخازن ونقاط البيع والفواتير الإلكترونية المتكامل - نطاق mccsale.vercel.app",
  "type": "module",
  "scripts": {
    "dev": "vite --port=3000 --host=0.0.0.0",
    "build": "vite build",
    "preview": "vite preview",
    "lint": "tsc --noEmit"
  },
  "dependencies": {
    "@google/genai": "^2.4.0",
    "@tailwindcss/vite": "^4.1.14",
    "@types/jsbarcode": "^3.11.4",
    "@vitejs/plugin-react": "^5.0.4",
    "@zxing/browser": "^0.2.1",
    "@zxing/library": "^0.23.0",
    "dotenv": "^17.2.3",
    "express": "^4.21.2",
    "html2canvas": "^1.4.1",
    "jsbarcode": "^3.12.3",
    "jspdf": "^4.2.1",
    "jszip": "^3.10.1",
    "lucide-react": "^0.546.0",
    "motion": "^12.23.24",
    "qrcode": "^1.5.4",
    "react": "^19.0.1",
    "react-dom": "^19.0.1",
    "recharts": "^3.10.1",
    "vite": "^6.2.3",
    "xlsx": "^0.18.5"
  },
  "devDependencies": {
    "@types/express": "^4.17.21",
    "@types/node": "^22.14.0",
    "@types/qrcode": "^1.5.6",
    "autoprefixer": "^10.4.21",
    "esbuild": "^0.25.0",
    "tailwindcss": "^4.1.14",
    "tsx": "^4.21.0",
    "typescript": "~5.8.2",
    "vite": "^6.2.3"
  }
}
# 🚀 الدليل الشامل لرفع وتشغيل النظام على أي استضافة ودومين

مرحباً بك! هذه الحزمة الكاملة تحتوي على النظام الجاهز للتشغيل والرفع على أي استضافة (cPanel, Apache, Nginx, Vercel, Netlify) مع قاعدة البيانات والدومين.

---

## ⚡ الخيار 1: الرفع على استضافة cPanel / Shared Hosting (Public_html)
1. افتح لوحة تحكم استضافتك (cPanel) وادخل إلى **مدير الملفات (File Manager)**.
2. توجه إلى مجلد موقعك الرئيسي: `public_html`.
3. اضغط على **رفع (Upload)** واختر ملف الـ ZIP هذا.
4. بعد الرفع، اضغط بالزر الأيمن على الملف واختر **استخراج (Extract)**.
5. تأكد من ظهور ملف `index.html` ومجلد `assets/` وملف `.htaccess` داخل `public_html`.
6. افتح دومين موقعك في المتصفح، وسيعمل النظام فوراً بكامل ألوانه وتنسيقاته!

> 💡 **ملاحظة:** ملف `.htaccess` المضمن يقوم تلقائياً بضبط مسارات النظام (SPA Routing) حتى تعمل روابط الكاشير والمسارات بدون ظهور أي خطأ 404.

---

## ⚡ الخيار 2: الرفع على Vercel (والدومين التلقائي https://mccsale.vercel.app)
1. فك ضغط هذا المجلد على جهازك.
2. افتح صفحة السحب والإفلات: **[https://vercel.com/new/drop](https://vercel.com/new/drop)**.
3. اسحب وأفلت المجلد المفكوك في الصفحة.
4. في خانة Project Name اكتب: `mccsale`.
5. ستحصل فوراً على الدومين المباشر: **https://mccsale.vercel.app** مع شهادة أمان SSL مجانية ومجددة تلقائياً.

---

## ⚡ الخيار 3: الرفع على استضافة Netlify
1. افتح موقع **[https://app.netlify.com/drop](https://app.netlify.com/drop)**.
2. اسحب المجلد المفكوك وأفلته، وسيعمل النظام فوراً بفضل ملف `_redirects` المرفق.

---

## 💻 الخيار 4: التجربة المحلية على جهاز الكمبيوتر
يمكنك تجربة النظام محلياً بأي من الطرق التالية:
- **باستخدام Python:** داخل المجلد افتح Terminal واكتب: `python -m http.server 3000` ثم افتح `http://localhost:3000`.
- **باستخدام Node.js:** اكتب: `npx serve .` ثم افتح الرابط المعروض.
- **باستخدام XAMPP:** ضع محتويات المجلد داخل `C:\xampp\htdocs\mccsale` وافتح `http://localhost/mccsale`.

---

## 🎯 روابط تشغيل الكاشير المباشرة على الدومين:
- **رابط الكاشير السريع:** `https://yourdomain.com/?mode=cashier`
- **رابط الكاشير التوافقي مع كروم:** `https://yourdomain.com/#cashier`

{
  "compilerOptions": {
    "target": "ES2022",
    "experimentalDecorators": true,
    "useDefineForClassFields": false,
    "module": "ESNext",
    "lib": [
      "ES2022",
      "DOM",
      "DOM.Iterable"
    ],
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "isolatedModules": true,
    "moduleDetection": "force",
    "allowJs": true,
    "jsx": "react-jsx",
    "paths": {
      "@/*": [
        "./*"
      ]
    },
    "allowImportingTsExtensions": true,
    "noEmit": true
  }
}

{
  "framework": "vite",
  "buildCommand": "npm run build",
  "outputDirectory": "dist",
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ],
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "X-Frame-Options",
          "value": "SAMEORIGIN"
        },
        {
          "key": "Access-Control-Allow-Origin",
          "value": "*"
        },
        {
          "key": "Permissions-Policy",
          "value": "clipboard-write=(self), clipboard-read=(self)"
        }
      ]
    }
  ]
}
# 🚀 دليل نشر النظام على منصة Vercel وربط الدومين: https://mccsale.vercel.app

مرحباً بك! هذا المجلد يحتوي على كامل كود المصدر والإعدادات الجاهزة بنسبة 100% لنشر نظام المخازن ونقاط البيع (MCC Sale) على منصة Vercel وتفعيل الدومين **https://mccsale.vercel.app** بشكل تلقائي وسريع.

---

## ⚡ الطريقة الأولى: النشر التلقائي عبر موقع Vercel (موصى بها وبسيطة جداً)

### الخطوة 1: رفع المشروع على حسابك في GitHub
1. فك ضغط هذا المجلد على جهازك.
2. أنشئ مستودعاً جديداً (New Repository) في حسابك على GitHub باسم: `mccsale`
3. ارفع كافة الملفات الموجودة داخل هذا المجلد إلى المستودع.

### الخطوة 2: الاستيراد في Vercel (الحصول على الدومين تلقائياً)
1. افتح موقع **[https://vercel.com](https://vercel.com)** وسجل الدخول بحساب GitHub.
2. اضغط على زر **"Add New..."** ثم اختر **"Project"**.
3. اختر المستودع `mccsale` واضغط **"Import"**.
4. في خانة **Project Name**، تأكد أن الاسم هو: `mccsale`
   > 💡 **ملاحظة هامة:** تسمية المشروع باسم `mccsale` في Vercel تمنحك تلقائياً وبشكل فوري الدومين المطلوب:
   > **https://mccsale.vercel.app** دون أي خطوات إضافية!
5. اضغط على زر **"Deploy"** وسيقوم Vercel ببناء الموقع ونشره في أقل من دقيقة واحدة.

---

## 🛠️ الخطوة 3: التحقق من الدومين وتعديله (إذا كان اسم المشروع مختلفاً)
إذا كان اسم المشروع مختلفاً في Vercel، يمكنك إضافة الدومين بسهولة:
1. داخل لوحة تحكم مشروعك في Vercel، اضغط على **Settings** في الأعلى.
2. اختر من القائمة الجانبية **Domains**.
3. في المستطيل اكتب: `mccsale.vercel.app`
4. اضغط على زر **Add**. سيصبح الدومين فعالاً ومتصلاً بموقعك فوراً مع شهادة أمان SSL مجانية مجددة تلقائياً!

---

## 💻 الطريقة الثانية: النشر الفوري عبر سطر الأوامر (Vercel CLI)
إذا كنت تفضل استخدام سطر الأوامر (Terminal / CMD):

```bash
# 1. التثبيت لأداة Vercel
npm i -g vercel

# 2. الانتقال لمجلد المشروع المفكوك
cd mccsale-pos-system

# 3. تسجيل الدخول والنشر المباشر للمشروع
vercel --prod
```
* عند سؤالك عن اسم المشروع (Project Name)، اكتب: `mccsale`
* سيتم إنشاء الرابط فوراً: **https://mccsale.vercel.app**

---

## 🎯 روابط النظام الجاهزة بعد النشر على الدومين:
* **رابط لوحة التحكم والشاشة الرئيسية:**
  `https://mccsale.vercel.app`
* **رابط محطة الكاشير ونقاط البيع السريعة (POS):**
  `https://mccsale.vercel.app?mode=cashier`
  أو:
  `https://mccsale.vercel.app/#cashier`
* **رابط الدخول المباشر لوردية الكاشير:**
  `https://mccsale.vercel.app?role=cashier`

---

## 🛡️ ما الذي تم تجهيزه لك داخل هذا المجلد؟
1. **ملف `vercel.json`:** معد ومبرمج خصيصاً لإعادة توجيه كافة المسارات (SPA Rewrites) إلى `index.html` وضمان عدم ظهور صفحة 404 عند تحديث الصفحة أو فتح روابط الكاشير.
2. **عناوين الأمان والتوافق:** تم تفعيل أذونات الحافظة (Clipboard) ليعمل نسخ رابط الكاشير بكفاءة تامة على جوجل كروم وأوبرا وجميع المتصفحات.
3. **حفظ البيانات محلياً (LocalStorage Persistence):** النظام يعمل بكفاءة تامة دون الحاجة لخادم خلفي معقد، ويحفظ بيانات المخزون والمبيعات محلياً مع إمكانية أخذ نسخ احتياطية بضغطة زر.
4. **تكامل هيئة الزكاة والضريبة والجمارك (ZATCA Phase 2):** شاشات إعدادات المنشأة ومفاتيح التشفير ECDSA والشهادات الرقمية جاهزة ومدمجة.

import tailwindcss from '@tailwindcss/vite';
import react from '@vitejs/plugin-react';
import { fileURLToPath } from 'url';
import path from 'path';
import { defineConfig } from 'vite';

const __dirname = path.dirname(fileURLToPath(import.meta.url));

export default defineConfig(() => {
  return {
    base: '/',
    plugins: [react(), tailwindcss()],
    resolve: {
      alias: {
        '@': path.resolve(__dirname, '.'),
      },
    },
    build: {
      outDir: 'dist',
      assetsDir: 'assets',
      emptyOutDir: true,
      sourcemap: false,
      minify: 'esbuild' as const,
      chunkSizeWarningLimit: 3500,
      rollupOptions: {
        output: {
          entryFileNames: 'assets/[name].js',
          chunkFileNames: 'assets/[name].js',
          assetFileNames: 'assets/[name].[ext]',
        },
      },
    },
    server: {
      port: 3000,
      host: '0.0.0.0',
    },
    preview: {
      port: 3000,
      host: '0.0.0.0',
    },
  };
});

# 🚀 الدليل الشامل لرفع وتشغيل النظام على أي استضافة ودومين

مرحباً بك! هذه الحزمة الكاملة تحتوي على النظام الجاهز للتشغيل والرفع على أي استضافة (cPanel, Apache, Nginx, Vercel, Netlify) مع قاعدة البيانات والدومين.

---

## ⚡ الخيار 1: الرفع على استضافة cPanel / Shared Hosting (Public_html)
1. افتح لوحة تحكم استضافتك (cPanel) وادخل إلى **مدير الملفات (File Manager)**.
2. توجه إلى مجلد موقعك الرئيسي: `public_html`.
3. اضغط على **رفع (Upload)** واختر ملف الـ ZIP هذا.
4. بعد الرفع، اضغط بالزر الأيمن على الملف واختر **استخراج (Extract)**.
5. تأكد من ظهور ملف `index.html` ومجلد `assets/` وملف `.htaccess` داخل `public_html`.
6. افتح دومين موقعك في المتصفح، وسيعمل النظام فوراً بكامل ألوانه وتنسيقاته!

> 💡 **ملاحظة:** ملف `.htaccess` المضمن يقوم تلقائياً بضبط مسارات النظام (SPA Routing) حتى تعمل روابط الكاشير والمسارات بدون ظهور أي خطأ 404.

---

## ⚡ الخيار 2: الرفع على Vercel (والدومين التلقائي https://mccsale.vercel.app)
1. فك ضغط هذا المجلد على جهازك.
2. افتح صفحة السحب والإفلات: **[https://vercel.com/new/drop](https://vercel.com/new/drop)**.
3. اسحب وأفلت المجلد المفكوك في الصفحة.
4. في خانة Project Name اكتب: `mccsale`.
5. ستحصل فوراً على الدومين المباشر: **https://mccsale.vercel.app** مع شهادة أمان SSL مجانية ومجددة تلقائياً.

---

## ⚡ الخيار 3: الرفع على استضافة Netlify
1. افتح موقع **[https://app.netlify.com/drop](https://app.netlify.com/drop)**.
2. اسحب المجلد المفكوك وأفلته، وسيعمل النظام فوراً بفضل ملف `_redirects` المرفق.

---

## 💻 الخيار 4: التجربة المحلية على جهاز الكمبيوتر
يمكنك تجربة النظام محلياً بأي من الطرق التالية:
- **باستخدام Python:** داخل المجلد افتح Terminal واكتب: `python -m http.server 3000` ثم افتح `http://localhost:3000`.
- **باستخدام Node.js:** اكتب: `npx serve .` ثم افتح الرابط المعروض.
- **باستخدام XAMPP:** ضع محتويات المجلد داخل `C:\xampp\htdocs\mccsale` وافتح `http://localhost/mccsale`.

---

## 🎯 روابط تشغيل الكاشير المباشرة على الدومين:
- **رابط الكاشير السريع:** `https://yourdomain.com/?mode=cashier`
- **رابط الكاشير التوافقي مع كروم:** `https://yourdomain.com/#cashier`
