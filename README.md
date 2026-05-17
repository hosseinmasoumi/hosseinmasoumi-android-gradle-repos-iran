# 📦 مخازن Gradle/Maven برای توسعه‌دهندگان اندروید در ایران 🇮🇷

به دلیل **تحریم‌ها و فیلترینگ**، خیلی وقت‌ها Gradle در Android Studio نمی‌تواند وابستگی‌ها را دانلود کند و خطاهایی مثل `Could not resolve`، `403` یا `timeout` نمایش داده می‌شود.

این ریپو شامل لیستی از **مخازن (Repositories)** و **میرورها (Mirrors)** است که به شما کمک می‌کند این مشکل را برطرف کنید.

---

## 🚀 نحوه استفاده

فایل `settings.gradle.kts` پروژه‌ات را با محتوای زیر جایگزین یا آپدیت کن:

```kotlin
pluginManagement {
    repositories {
        // ─── Mirror های ایرانی ───────────────────────────────────────
        maven { url = uri("https://maven.myket.ir") }
        maven { url = uri("https://maven.devneeds.ir") }
        maven { url = uri("https://gradle.iranrepo.ir") }
        maven { url = uri("https://gradle.jamko.ir") }
        maven { url = uri("https://en-mirror.ir") }
        maven { url = uri("https://archive.ito.gov.ir/gradle/maven-plugin/") }

        // ─── Mirror های چین (Aliyun) ─────────────────────────────────
        maven { url = uri("https://maven.aliyun.com/repository/gradle-plugin") }
        maven { url = uri("https://maven.aliyun.com/repository/google") }

        // ─── منابع رسمی (Fallback) ────────────────────────────────────
        google {
            content {
                includeGroupByRegex("com\\.android.*")
                includeGroupByRegex("com\\.google.*")
                includeGroupByRegex("androidx.*")
            }
        }
        gradlePluginPortal()
        mavenCentral()
    }
}

dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)

    repositories {
        // ─── Mirror های ایرانی ───────────────────────────────────────
        maven { url = uri("https://maven.myket.ir") }
        maven { url = uri("https://maven.devneeds.ir") }
        maven { url = uri("https://gradle.iranrepo.ir") }
        maven { url = uri("https://gradle.jamko.ir") }
        maven { url = uri("https://en-mirror.ir") }
        maven { url = uri("https://archive.ito.gov.ir/gradle/maven-plugin/") }

        // ─── Mirror های چین (Aliyun) ─────────────────────────────────
        maven { url = uri("https://maven.aliyun.com/repository/public") }
        maven { url = uri("https://maven.aliyun.com/repository/central") }
        maven { url = uri("https://maven.aliyun.com/repository/google") }

        // ─── منابع رسمی (Fallback) ────────────────────────────────────
        google()
        mavenCentral()
        maven { url = uri("https://jitpack.io") }
    }
}

rootProject.name = "YourProjectName"
include(":app")
```

---

## 📋 فهرست مخازن

| مخزن | نوع | کاربرد |
|------|-----|---------|
| `maven.myket.ir` | 🇮🇷 ایرانی | Mirror عمومی |
| `maven.devneeds.ir` | 🇮🇷 ایرانی | Mirror عمومی |
| `gradle.iranrepo.ir` | 🇮🇷 ایرانی | Mirror عمومی |
| `gradle.jamko.ir` | 🇮🇷 ایرانی | Mirror عمومی |
| `en-mirror.ir` | 🇮🇷 ایرانی | Mirror عمومی |
| `archive.ito.gov.ir` | 🇮🇷 دولتی | آرشیو ITO |
| `maven.aliyun.com` | 🇨🇳 چین | Mirror Aliyun |
| `jitpack.io` | 🌐 بین‌المللی | کتابخانه‌های GitHub |

---

## ⚠️ نکات مهم

- ترتیب مخازن مهم است؛ Gradle از **بالا به پایین** جستجو می‌کند.
- منابع رسمی (`google()`, `mavenCentral()`) را **همیشه** در انتها نگه دار تا fallback باشند.
- در صورت اضافه کردن مخزن جدید، حتماً آن را هم در `pluginManagement` و هم در `dependencyResolutionManagement` اضافه کن.

---

## 🤝 مشارکت

اگه میروری پیدا کردی که کار می‌کنه یا یه میرور از کار افتاده، خوشحال می‌شم Pull Request بزنی!
