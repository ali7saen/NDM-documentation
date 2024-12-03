# **الدليل المختصر لجهاز NMD**
---

تمت كتابة هذا التوثيق بناءً على النسخة الأصلية المقدمة من الشركة، حيث تم اختصار أهم الأجزاء وتبسيطها في هذا التوثيق. مع ذلك، يُنصح بالرجوع إلى التوثيق الأصلي في بعض الحالات للحصول على تفاصيل أعمق.
تم تلخيص هذا التوثيق من قبل المبرمج علي حسين باستخدام ChatGPT.
لأي مقترحات أو استفسارات، يمكنكم التواصل مع علي حسين.

---

## **نظرة عامة على الوصف المادي لجهاز NMD**

### **مقدمة**

يشرح هذا القسم البنية المادية لجهاز **NMD (Note Management Device - جهاز إدارة الأوراق النقدية)**، موضحًا كيفية تواصل مكوناته الداخلية مع بعضها البعض ومع الأنظمة الخارجية. يهدف هذا الدليل إلى تقديم صورة مبسطة تساعد المطورين والمهندسين في فهم هيكل الجهاز وآلية عمله.

### **الهيكل الداخلي للجهاز**

1. **المكونات الأساسية:**
   - **وحدة المعالجة المركزية (CPU - وحدة المعالجة المركزية):**
     - تُدير جميع العمليات الداخلية للجهاز.
     - تتولى معالجة الأوامر القادمة من الشبكة.
   - **وحدة التغذية الكهربائية (وحدة التغذية الكهربائية):**
     - تزود الجهاز بالطاقة اللازمة لتشغيل الوحدات المختلفة.
   - **وحدة التحكم بالكاسيت (وحدة التحكم بالكاسيت):**
     - تتحكم في الكاسيتات المسؤولة عن الأوراق النقدية.

2. **وظائف الوحدات:**
   - **وحدة الحساسات (الحساسات - حساسات):**
     - تتبع حركة الأوراق النقدية وتتحقق من مواضعها.
   - **المحركات (المحركات - محركات):**
     - تحرك الأوراق النقدية داخل الجهاز لنقلها بين الوحدات المختلفة.

---

### **واجهة الاتصال**

1. **البروتوكولات المستخدمة:**
   - **RS-232 (الاتصال التسلسلي) (بروتوكول الاتصال التسلسلي):** للتواصل بين الجهاز الرئيسي والشبكة.
   - **RS-485 (الاتصال الداخلي) (بروتوكول الاتصال الداخلي):** للتواصل بين المكونات الداخلية للجهاز.

2. **إشارات التحكم:**
   - **RTS (طلب الإرسال - طلب الإرسال):** تُستخدم للإشارة إلى الجاهزية لإرسال البيانات.
   - **CTS (إذن الإرسال - إذن الإرسال):** تُستخدم للإشارة إلى السماح باستقبال البيانات.

3. **التوصيلات المادية:**
   - يتم توصيل المكونات الداخلية باستخدام كابلات معيارية.
   - يحتوي الجهاز على واجهات مثل **CAN-BUS (نظام اتصال داخلي) (نظام اتصال داخلي للبيانات)** لربط الوحدات.

---

## **نظرة عامة على الوصف المنطقي لجهاز NMD**

### **مقدمة**

يشرح الوصف المنطقي كيفية عمل جهاز **NMD** على مستوى البرمجيات والبروتوكولات، ويوضح العلاقة بين الأوامر الصادرة من الشبكة والردود التي يقدمها الجهاز. يتم استخدام هذا الوصف لتسهيل فهم عملية الاتصال وتدفق البيانات داخل الجهاز ومع النظام الخارجي.

### **آلية العمل**

1. **البروتوكول المنطقي:**
   - يعتمد الاتصال بين الشبكة وجهاز NMD على آلية تبادل أوامر وردود.
   - يجب أن تبدأ الشبكة دائمًا بإرسال الأوامر، ويتبعها الجهاز برد مناسب بناءً على الحالة.

2. **صيغة الأوامر والردود:**
   - كل رسالة تتبع تنسيقًا محددًا يتضمن:
     - **كود العملية (Operation Code):** يحدد نوع العملية.
     - **البيانات (Data):** إذا تطلب الأمر.
     - **LRC (Longitudinal Redundancy Check - التحقق الطولي):** لضمان سلامة البيانات.
     - **EOM (End of Message - نهاية الرسالة):** للإشارة إلى اكتمال الرسالة.

3. **التحقق من الأخطاء:**
   - يتم استخدام **LRC** لاكتشاف وتصحيح الأخطاء أثناء نقل البيانات.

---

## **نظرة عامة على الأوامر لجهاز NMD**

### **أوامر شائعة الاستخدام**

| **الكود** | **الوصف**                 | **الزمن المطلوب** |
|-----------|---------------------------|-------------------|
| `X30`     | RESET                     | 20-180 ثانية      |
| `X32`     | MOVE FORWARD              | 180 ثانية         |
| `X33`     | DELIVER                   | 20-180 ثانية      |
| `X38`     | OPEN CASSETTE             | 180 ثانية         |
| `X37`     | CLOSE CASSETTE            | 20-180 ثانية      |

### **شرح الأوامر**

1. **RESET (X30):**
   - يُستخدم لإعادة تهيئة الجهاز بعد حدوث خطأ أو عطل.
   - يساعد في مسح جميع الأخطاء واستعادة الحالة الافتراضية للجهاز.

2. **MOVE FORWARD (X32):**
   - يُستخدم لتحريك الأوراق النقدية من الكاسيت إلى منطقة التسليم.
   - يتطلب تحديد عدد الأوراق النقدية المراد تحريكها.

3. **DELIVER (X33):**
   - يُستخدم لتسليم الأوراق النقدية التي تم تحريكها إلى المستخدم.

4. **OPEN CASSETTE (X38):**
   - يفتح الكاسيتات للسماح بالتعامل اليدوي أو الصيانة.

5. **CLOSE CASSETTE (X37):**
   - يغلق الكاسيتات بعد الانتهاء من العمليات أو الصيانة.

### **طريقة إرسال الأوامر**

- يتم إرسال الأوامر باستخدام التنسيق التالي:
  - **كود العملية (Operation Code):** يُحدد نوع العملية.
  - **البيانات (Data):** تُضاف إذا لزم الأمر (مثل عدد الأوراق النقدية).
  - **LRC (Longitudinal Redundancy Check):** لضمان صحة البيانات.
  - **EOM (End of Message):** لإنهاء الرسالة.

### **أمثلة على الأوامر**

- إرسال أمر RESET:
  ```
  X30<CR>
  ```

- إرسال أمر MOVE FORWARD لتحريك 5 أوراق نقدية:
  ```
  X32 05<CR>
  ```

---

### **كود Java للاتصال بجهاز NMD وإرسال الأوامر**

#### **الاتصال بجهاز NMD:**

```java
import gnu.io.*;
import java.io.*;

public class NMDCommunication {

    public static void main(String[] args) {
        try {
            // تحديد المنفذ
            CommPortIdentifier portId = CommPortIdentifier.getPortIdentifier("COM1");

            // فتح الاتصال بالمنفذ
            SerialPort serialPort = (SerialPort) portId.open("NMDCommunication", 2000);

            // إعدادات الاتصال
            serialPort.setSerialPortParams(9600, SerialPort.DATABITS_7, SerialPort.STOPBITS_1, SerialPort.PARITY_EVEN);

            OutputStream output = serialPort.getOutputStream();
            InputStream input = serialPort.getInputStream();

            // إرسال الأمر (مثال: RESET)
            String command = "X30\n";
            output.write(command.getBytes());

            // استقبال الرد
            byte[] buffer = new byte[256];
            int len = input.read(buffer);
            System.out.println("Response: " + new String(buffer, 0, len));

            // إغلاق الاتصال
            serialPort.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### **شرح الكود:**
1. **فتح الاتصال:** يتم فتح منفذ تسلسلي باستخدام مكتبة RXTX.
2. **إعداد الاتصال:** يتم ضبط معدل الباود، عدد البتات، والتحقق من التماثل.
3. **إرسال الأوامر:** يتم إرسال الأوامر كـ String إلى الجهاز.
4. **استقبال الردود:** يتم قراءة الردود من الجهاز وتحليلها.

---
## **التعامل مع الردود وأكواد الحالة لجهاز NMD**
الردود الصادرة عن جهاز NMD تحتوي على أكواد الحالة (Status Codes) التي توضح نتيجة الأوامر المرسلة. فهم أكواد الحالة يساعد على تحليل الأخطاء وضمان تنفيذ العمليات بشكل صحيح.

---

### **هيكل الرد**

- **الرد يتضمن:**
  - **Status Code (كود الحالة):** يشير إلى نجاح أو فشل العملية.
  - **تفاصيل إضافية (اختيارية):** توفر معلومات إضافية حول الخطأ أو الحالة.
  - **EOM (End of Message - نهاية الرسالة):** للإشارة إلى اكتمال الرد.

---

### **أكواد الحالة الشائعة ومعانيها**

| **كود الحالة** | **الوصف**                             | **الإجراء المطلوب**             |
|-----------------|-------------------------------------|----------------------------------|
| `X30`          | العملية تمت بنجاح                   | لا يوجد إجراء إضافي.            |
| `X31`          | مستوى الأوراق النقدية منخفض          | تعبئة الأوراق النقدية.          |
| `X32`          | الكاسيت فارغ                        | تحقق من الكاسيت وأعد تعبئته.    |
| `X37`          | خطأ في الاتصال                      | تحقق من الكابلات وإعدادات الاتصال. |
| `X38`          | أمر غير صحيح                        | تحقق من صيغة الأمر المرسل.     |

---

### **كود Java لاستقبال الردود وتحليلها**

```java
import gnu.io.*;
import java.io.*;

public class NMDResponseHandler {

    public static void main(String[] args) {
        try {
            // تحديد المنفذ
            CommPortIdentifier portId = CommPortIdentifier.getPortIdentifier("COM1");

            // فتح الاتصال بالمنفذ
            SerialPort serialPort = (SerialPort) portId.open("NMDResponseHandler", 2000);

            // إعدادات الاتصال
            serialPort.setSerialPortParams(9600, SerialPort.DATABITS_7, SerialPort.STOPBITS_1, SerialPort.PARITY_EVEN);

            OutputStream output = serialPort.getOutputStream();
            InputStream input = serialPort.getInputStream();

            // إرسال الأمر (مثال: RESET)
            String command = "X30\n";
            output.write(command.getBytes());

            // استقبال الرد
            byte[] buffer = new byte[256];
            int len = input.read(buffer);
            String response = new String(buffer, 0, len);

            // تحليل الرد
            if (response.startsWith("X30")) {
                System.out.println("العملية تمت بنجاح.");
            } else if (response.startsWith("X31")) {
                System.out.println("مستوى الأوراق النقدية منخفض. يُرجى تعبئة الجهاز.");
            } else if (response.startsWith("X32")) {
                System.out.println("الكاسيت فارغ. يُرجى إعادة تعبئة الكاسيت.");
            } else if (response.startsWith("X37")) {
                System.out.println("خطأ في الاتصال. تحقق من الكابلات وإعدادات الاتصال.");
            } else if (response.startsWith("X38")) {
                System.out.println("أمر غير صحيح. تحقق من صيغة الأمر المرسل.");
            } else {
                System.out.println("رد غير معروف: " + response);
            }

            // إغلاق الاتصال
            serialPort.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

### **شرح الكود**

1. **إرسال الأمر:** يتم إرسال أمر إلى الجهاز باستخدام منفذ تسلسلي.
2. **استقبال الرد:** يتم قراءة الرد وتحويله إلى نص يمكن تحليله.
3. **تحليل الرد:**
   - يتم مقارنة كود الحالة في الرد بالقيم الشائعة.
   - عرض رسالة توضيحية بناءً على الكود المستلم.
4. **إغلاق الاتصال:** بعد استلام الرد وتحليله، يتم إغلاق الاتصال بالجهاز.

---

## **ترميز الكاسيتات وLEDs في جهاز NMD**
### **ترميز الكاسيتات (Coding of Note Cassette/Reject Vault)**

- يتم تعريف كل كاسيت في الجهاز باستخدام رقم تعريف فريد (**ID-Number**) مكون من 5 أرقام.
- في أول استخدام للكاسيت، يجب برمجته بهذا الرقم، وعادة ما يتم ذلك في المصنع.

#### **استخدامات الأرقام التعريفية**

- يتم استخدام الأرقام التعريفية للكاسيتات والهوبّرات (Hopper Numbers) لتتبع الحركات النقدية داخل الجهاز.
- **Hopper Number 0** مخصص دائمًا لكاسيت الرفض.

#### **ترميز الكاسيتات داخل الجهاز**

- يتم إدخال الكاسيت في الجهاز، ويتولى النظام تلقائيًا تعيين الرقم التعريفي للكاسيت.
- بعد تعيين الرقم، يجب إصدار أمر `X37` **(Close Cassette)** لإغلاق الكاسيت وجعله جاهزًا للعمل.

#### **إعدادات العملة وحجم الأوراق النقدية**

- يمكن إعداد العملة وحجم الأوراق النقدية باستخدام الأوامر التالية:
  - `WD/9H27` لتحديد العملة.
  - `WD/9H28` لتحديد رقم تعريف الكاسيت.
  - `WD/9H29` لتحديد حجم الأوراق النقدية.

---

### **تفسير LEDs في جهاز CMC200**

#### **الوضعيات المختلفة للـ LEDs**

1. **التشغيل (Start-up):**
   - تضيء كلتا الـ LEDs أثناء تشغيل جهاز CMC200.

2. **التشغيل الطبيعي (Machine is operational):**
   - وميض LED واحد بتردد 1 هرتز.

3. **وجود خطأ (Error detected):**
   - وميض كلتا الـ LEDs بالتسلسل لتحديد رمز الخطأ الداخلي.

#### **آلية تحديد الأخطاء باستخدام LEDs**

- يتم عرض رقم المهمة (Task Number) ورمز الخطأ (Error Code) باستخدام وميض LED:
  - **LED الأول:** يحدد عدد العشرات في رقم المهمة.
  - **LED الثاني:** يحدد الوحدات.

- بعد عرض رمز الخطأ، تومض كلتا الـ LEDs كفاصل قبل تكرار الرمز.

#### **الخطوات عند اكتشاف خطأ**

- تحقق من رمز الخطأ الظاهر.
- راجع دليل المستخدم للحصول على تفاصيل الخطأ.
- قم بالإجراءات التصحيحية بناءً على التوصيات.

---


## **هيكل الأوامر والردود لجهاز NMD**

### **نقل البيانات (Data Transmission)**

- يتم نقل البيانات بين جهاز NMD والشبكة باستخدام منفذ تسلسلي (**V.24 Port**).
- يعتمد الاتصال على إرسال واستقبال الرسائل بشكل أزواج: **Command-Reply Messages**.

---

### **تنسيق الرسائل (Message Format)**

#### **تنسيق الأوامر (Commands Format):**

| **العنصر** | **الوصف**                     |
|------------|-----------------------------|
| `C`        | كود العملية (Operation Code) |
| `D`        | البيانات (Data)              |
| `L`        | فحص التكرار الطولي (LRC)     |
| `E`        | نهاية الرسالة (EOM)          |

- أمثلة على الأوامر:
  - `X32`: تحريك الأوراق النقدية.
  - `X33`: تسليم الأوراق النقدية.
  - `X57 X44`: قراءة البيانات.

---

### **تنسيق الردود (Status Reply Format)**

| **العنصر** | **الوصف**                     |
|------------|-----------------------------|
| `S`        | كود الحالة (Status Code)     |
| `D`        | البيانات (Data)              |
| `L`        | فحص التكرار الطولي (LRC)     |
| `E`        | نهاية الرسالة (EOM)          |

#### **كود الحالة (Status Code):**
- يتم تحديد نجاح أو فشل العملية بناءً على الكود المرسل.

### **LRC (Longitudinal Redundancy Check):**
- تُستخدم لضمان دقة البيانات المرسلة والمستقبلة.

---

### **نظرة عامة على الأوامر (Commands Overview)**

| **كود العملية** | **الوصف**                                   | **المدة القصوى للتنفيذ** |
|------------------|-------------------------------------------|-------------------------|
| `X30`           | إعادة ضبط الجهاز (RESET)                  | 180 ثانية              |
| `X32`           | تحريك الأوراق النقدية (MOVE FORWARD)      | 180 ثانية              |
| `X33`           | تسليم الأوراق النقدية (DELIVER)           | 180 ثانية              |
| `X34`           | رفض الأوراق النقدية (REJECT)              | 180 ثانية              |
| `X35`           | قراءة رقم تعريف الكاسيت (READ CASS-ID)    | 20 ثانية               |
| `X36`           | التحقق من الأوراق المسلمة (CHECK DELIVERED NOTES) | 20 ثانية          |
| `X37`           | إغلاق الكاسيت (CLOSE CASSETTE)            | 180 ثانية              |
| `X38`           | فتح الكاسيت (OPEN CASSETTE)               | 180 ثانية              |
| `X39`           | قراءة سجل الرفض (READ REJECT TRACE)       | 5 ثوانٍ                |
| `X3A`           | التحقق من وحدة الإخراج (CHECK BUNDLE OUTPUT UNIT) | 5 ثوانٍ         |
| `X41`           | قراءة رقم البرنامج (READ PROG-ID)         | 5 ثوانٍ                |
| `X44`           | سحب الأوراق النقدية (RETRACT)             | 180 ثانية              |
| `X47`           | إرسال بيانات الاختبار الذاتي (SEND SELFTEST DATA) | 20 ثانية          |
| `X4B`           | إعادة إرسال الرسالة الأخيرة (RESEND LAST MESSAGE) | 5 ثوانٍ         |
| `X51`           | التحقق من حالة NMD (CHECK NMD STATUS)     | 20 ثانية               |
| `X53`           | التحقق من الأوراق المكدسة (CHECK STACKED NOTES) | 20 ثانية          |
| `X52 X44`       | قراءة البيانات (READ DATA)                | 20 ثانية               |
| `X57 X44`       | كتابة البيانات (WRITE DATA)               | 60 ثانية               |

---

### **تصنيف الأوامر (Commands Categories)**

1. **أوامر الحركة (Movement Commands):**
   - `X30`: إعادة ضبط.
   - `X32`: تحريك الأوراق النقدية.
   - `X33`: تسليم الأوراق النقدية.
   - `X34`: رفض الأوراق النقدية.
   - `X37`: إغلاق الكاسيت.
   - `X38`: فتح الكاسيت.

2. **أوامر غير الحركة (Non-Movement Commands):**
   - `X35`: قراءة رقم تعريف الكاسيت.
   - `X36`: التحقق من الأوراق المسلمة.
   - `X39`: قراءة سجل الرفض.
   - `X3A`: التحقق من وحدة الإخراج.
   - `X41`: قراءة رقم البرنامج.
   - `X47`: إرسال بيانات الاختبار الذاتي.
   - `X4B`: إعادة إرسال الرسالة الأخيرة.
   - `X51`: التحقق من حالة الجهاز.
   - `X53`: التحقق من الأوراق المكدسة.
   - `X52 X44`: قراءة البيانات.
   - `X57 X44`: كتابة البيانات.

---

### **أمثلة على الأوامر والردود**

#### **مثال 1: أمر تحريك الأوراق النقدية (MOVE FORWARD)**

**الأمر:**
```
C: X32
D: 00205 (عدد الأوراق المطلوبة)
L: LRC المحسوب
E: <CR>
```

**الرد:**
```
S: X30 (نجاح العملية)
H: X31 (رقم الهوبّر)
F: X00 (حالة الهوبّر)
N: 00205 (عدد الأوراق المنقولة)
L: LRC المحسوب
E: <CR>
```

**شرح الرد:**
- `S: X30`: العملية تمت بنجاح.
- `H: X31`: الأوراق تم أخذها من الهوبّر رقم 1.
- `N: 00205`: تم نقل 205 أوراق نقدية بنجاح.

---

#### **مثال 2: أمر قراءة رقم تعريف الكاسيت (READ CASS-ID)**

**الأمر:**
```
C: X35
L: LRC المحسوب
E: <CR>
```

**الرد:**
```
S: X30 (نجاح العملية)
D: 12345 (رقم تعريف الكاسيت)
L: LRC المحسوب
E: <CR>
```

**شرح الرد:**
- `S: X30`: العملية تمت بنجاح.
- `D: 12345`: رقم تعريف الكاسيت هو 12345.
---

## **متطلبات تطوير تطبيق مكتبي للتعامل مع جهاز NMD باستخدام Java**

### **المتطلبات الأساسية**

#### **1. بنية التطبيق (Application Structure):**

- **الطبقات الأساسية:**
  - **واجهة المستخدم (UI):** لتقديم واجهة تفاعلية للمستخدم لإرسال واستقبال الأوامر.
  - **طبقة الاتصال (Communication Layer):** للتعامل مع إرسال واستقبال البيانات عبر المنفذ التسلسلي.
  - **طبقة الأعمال (Business Logic Layer):** لمعالجة البيانات وإدارة أوامر الجهاز.
  - **طبقة الخدمات (Service Layer):** لتنفيذ العمليات الخاصة بجهاز NMD مثل إرسال الأوامر وتحليل الردود.

---

### **المكتبات المطلوبة**

#### **1. مكتبات Java الأساسية:**
- **`javax.comm`**: لإدارة الاتصال عبر المنافذ التسلسلية.
- **`RXTX`**: مكتبة شائعة لتوفير وظائف الاتصال التسلسلي في Java.

#### **2. مكتبات إضافية:**
- **`Log4j`**: لتسجيل العمليات والأخطاء.
- **`Jackson`**: لتحليل البيانات إذا كانت تأتي بتنسيق JSON (اختياري).

---

### **شيفرات برمجية (Code Snippets)**

#### **1. إعداد الاتصال بجهاز NMD**
```java
import gnu.io.CommPort;
import gnu.io.CommPortIdentifier;
import gnu.io.SerialPort;
import java.io.OutputStream;

public class NMDConnection {

    private SerialPort serialPort;

    public void connect(String portName) throws Exception {
        CommPortIdentifier portIdentifier = CommPortIdentifier.getPortIdentifier(portName);
        if (portIdentifier.isCurrentlyOwned()) {
            throw new Exception("Port is currently in use");
        } else {
            CommPort commPort = portIdentifier.open(this.getClass().getName(), 2000);

            if (commPort instanceof SerialPort) {
                serialPort = (SerialPort) commPort;
                serialPort.setSerialPortParams(9600, SerialPort.DATABITS_7, SerialPort.STOPBITS_1, SerialPort.PARITY_EVEN);
            } else {
                throw new Exception("Only serial ports are handled");
            }
        }
    }

    public OutputStream getOutputStream() throws Exception {
        if (serialPort != null) {
            return serialPort.getOutputStream();
        } else {
            throw new Exception("Serial port not initialized");
        }
    }
}
```

#### **2. إرسال أمر إلى جهاز NMD**
```java
public class NMDCommandSender {

    private NMDConnection connection;

    public NMDCommandSender(NMDConnection connection) {
        this.connection = connection;
    }

    public void sendCommand(String command) throws Exception {
        OutputStream outputStream = connection.getOutputStream();
        outputStream.write(command.getBytes());
        outputStream.flush();
    }
}
```

#### **3. استقبال الرد من جهاز NMD**
```java
import java.io.InputStream;

public class NMDResponseReceiver {

    private SerialPort serialPort;

    public NMDResponseReceiver(SerialPort serialPort) {
        this.serialPort = serialPort;
    }

    public String receiveResponse() throws Exception {
        InputStream inputStream = serialPort.getInputStream();
        byte[] buffer = new byte[256];
        int len = inputStream.read(buffer);
        return new String(buffer, 0, len);
    }
}
```

---

### **أمثلة على تنفيذ الأوامر**

#### **1. إرسال أمر MOVE FORWARD واستقبال الرد**
```java
public class NMDApplication {

    public static void main(String[] args) {
        try {
            // إنشاء الاتصال
            NMDConnection connection = new NMDConnection();
            connection.connect("COM1");

            // إرسال الأمر
            NMDCommandSender sender = new NMDCommandSender(connection);
            sender.sendCommand("X32 00205\r");

            // استقبال الرد
            NMDResponseReceiver receiver = new NMDResponseReceiver(connection.getSerialPort());
            String response = receiver.receiveResponse();

            // تحليل الرد
            System.out.println("Response: " + response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### **2. تحليل الردود والتعامل مع الأكواد**
```java
public class NMDResponseParser {

    public void parseResponse(String response) {
        char statusCode = response.charAt(0);

        switch (statusCode) {
            case '0':
                System.out.println("Success");
                break;
            case '1':
                System.out.println("Low Level");
                break;
            case '2':
                System.out.println("Empty Cassette");
                break;
            default:
                System.out.println("Unknown status code: " + statusCode);
        }
    }
}
```

---

### **ملاحظات**

1. **التهيئة:** تأكد من إعداد المنفذ التسلسلي بشكل صحيح.
2. **الأمان:** تأكد من تسجيل الأخطاء باستخدام مكتبة مثل Log4j لتسهيل التشخيص.
3. **الاختبار:** قم بمحاكاة أوامر وبيئات مختلفة لاختبار التطبيق بشكل شامل.

