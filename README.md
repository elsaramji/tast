# **🙂Project Architecture**

## **How build maintainable Project**

---

## **🧠 أولاً: ليه أصلاً نختار Architecture؟**

* **علشان تنظيم الكود**

* **تسهّل الاختبار (Testing)**

* **تسهّل الصيانة والتوسعة**

* **تخلي الفريق يشتغل على نفس الأساس**

---

## **✅ ثانيًا: العوامل اللي تحدد اختيارك:**

### **1\. حجم المشروع**

| الحجم | المعمارية المقترحة |
| ----: | ----: |
| **صغير** | **Provider / BLoC بسيط** |
| **متوسط** | **MVVM أو BLoC منظّم** |
| **كبير** | **Clean Architecture / TDD** |

---

### **2\. عدد المطورين**

* **لو شغال لوحدك: استخدم حاجة سريعة التنظيم (MVVM أو Riverpod).**

* **لو فريق كبير: استخدم Clean Architecture عشان التوزيع والتوسعة أسهل.**

---

### **3\. قابلية التوسع**

* **مشروع هيتوسع؟**  
   **استخدم Layered Architecture (زي Clean أو Hexagonal).**

* **مشروع مؤقت؟**  
   **استخدم Minimal Architecture (زي Feature-first \+ Provider أو Riverpod).**

---

### **4\. متطلبات المشروع (Offline, Auth, API, Cache...)**

* **لو المشروع فيه تعقيدات زي:**

  * **Offline support**

  * **Local \+ Remote data**

  * **Authentication**

  * **Business rules معقدة**

**يبقى Clean Architecture أو Domain-driven design أفضل.**

---

## **🔧 ثالثًا: أشهر المعماريات المستخدمة في Flutter**

| Architecture | لما تستخدمها | سهولة الفهم |
| ----: | ----: | ----: |
| **Provider (basic)** | **مشاريع صغيرة ومتوسطة** | **سهل** |
| **BLoC** | **مشاريع تحتاج فصل Presentation/Logic** | **متوسط** |
| **Riverpod** | **مشاريع تحتاج إدارة حالة مرنة وسهلة** | **سهل-متوسط** |
| **MVVM** | **لو عندك UI ثقيل وتفصل ViewModel** | **متوسط** |
| **Clean Architecture** | **مشاريع كبيرة فيها Layers متعددة** | **متقدم** |

---

## **👇 مثال عملي:**

### **مشروع بسيط (ToDo App):**

**استخدم Provider أو Riverpod**

### **مشروع متوسط (E-commerce app):**

**استخدم MVVM أو BLoC**

### **مشروع كبير (مثلاً LMS \- نظام تعليم):**

**استخدم Clean Architecture**

---

## **🔥 نصيحة:**

**ابني المعمارية حسب الحاجة مش حسب الترند.**  
 **يعني: مش لازم تبدأ Clean Architecture في مشروع بسيط هيتسلم بعد أسبوعين. خليك عملي.**

## **🧱 Clean Architecture في Flutter**

### **✅ ما هو الـ Clean Architecture؟**

**Clean Architecture هو نمط تصميم معماري هدفه الأساسي هو فصل الكود إلى طبقات واضحة بحيث كل طبقة لها مسؤولية محددة، وتكون منفصلة عن التفاصيل التقنية.**

### **🎯 هدفه الرئيسي:**

* **فصل الـ Business Logic عن UI.**

* **تسهيل الصيانة والاختبار.**

* **جعل المشروع قابل للتوسع.**

---

## **🧠 لماذا نستخدم Clean Architecture؟**

1. **سهولة الصيانة والتوسعة:**

   * **أي تعديلات أو إضافات مستقبلية بتكون محدودة في طبقة واحدة.**

2. **قابلية للاختبار (Testing):**

   * **تقدر تختبر الـ Use Cases بدون ما تعتمد على UI أو API.**

3. **تنظيم المشروع بشكل سهل الفهم:**

   * **لما حد يدخل على المشروع، يقدر يعرف فين الكود الخاص بالـ UI وفين الـ Logic.**

4. **سهولة التعاون بين الفريق:**

   * **تقدر تقسم الشغل على مطور UI، ومطور Business Logic، ومطور API.**

---

## **🧱 هيكل Clean Architecture في Flutter:**

**lib/**  
**├── core/              \# كود مشترك (ثوابت، أخطاء، مساعدات)**  
**├── features/**  
**│   └── feature\_name/**  
**│       ├── data/**  
**│       │   ├── models/**  
**│       │   ├── datasources/**  
**│       │   └── repositories\_impl/**  
**│       ├── domain/**  
**│       │   ├── entities/**  
**│       │   ├── repositories/**  
**│       │   └── usecases/**  
**│       └── presentation/**  
**│           ├── pages/**  
**│           ├── widgets/**  
**│           └── bloc/**  
**└── main.dart**

---

### **💡 الطبقات الثلاث:**

#### **1\. Domain Layer:**

* **تحتوي على:**

  * **Entities**

  * **UseCases**

  * **Repository Interfaces**  
* **لا تعتمد على أي طبقة تانية.**

#### **2\. Data Layer:**

* **تحتوي على:**

  * **Models**

  * **DataSources (API/Local)**

  * **Repositories Implementation**

* **تعتمد على Domain فقط.**

#### **3\. Presentation Layer:**

* **تحتوي على:**

  * **UI**

  * **Bloc / Cubit**

  * **Pages & Widgets**

* **تعتمد على Domain (تستخدم الـ UseCases).**

---

## **🤔 طيب إيه الفرق بين Clean Architecture و MVVM؟**

|  | Clean Architecture | MVVM |
| ----- | ----- | ----- |
| **التنظيم** | **طبقات واضحة (Data, Domain, UI)** | **Model \+ View \+ ViewModel** |
| **الـ Use Cases** | **موجودة في طبقة منفصلة** | **أحيانًا موجودة جوه ViewModel** |
| **قابلية التوسع** | **أعلى وأكثر مرونة** | **مرنة ولكن أقل على المشاريع الكبيرة** |
| **الالتزام بالفصل** | **صارم جدًا** | **مرن أكثر** |

### **📌 MVVM مناسب:**

* **للمشاريع المتوسطة.**

* **لو عايز ViewModel يتحكم في الـ State.**

* **لو مش محتاج Use Cases منفصلة.**

### **📌 Clean Architecture مناسب:**

* **للمشاريع الكبيرة أو اللي هتكبر.**

* **لو في فريق شغال.**

* **لو عندك Business Logic معقدة.**

---

## **✨ الخلاصة:**

* **Clean Architecture هو أسلوب قوي جدًا في التنظيم.**

* **مناسب جدًا لما المشروع يبدأ يكبر، أو في فريق.**

* **بيسهّل التوسعة، والاختبار، والقراءة.**

**ابني المشروع على قد حجمه، بس خليك جاهز تنقله لـ Clean Architecture بسهولة لما يحتاج.**

**Links:**  
**Omar Ahmed :[Clean Architecture deep dive \- بالعربي](https://www.youtube.com/watch?v=JJlS_UtlYLg)**  
**Medium :  [Clean Architecture in Flutter | MVVM | BloC | Dio | by Yamen Abdulrahman | Medium](https://medium.com/@yamen.abd98/clean-architecture-in-flutter-mvvm-bloc-dio-79b1615530e1)**  
**Meeting of the Giants : [Clean Architecture in Flutter with @OmarAhmedx14 & @AbdullahMansourAli](https://www.youtube.com/watch?v=5MzxXMNv9qg&t=1920s)**  
