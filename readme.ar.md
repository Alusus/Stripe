# Stripe
[[English]](readme.md)

<div dir=rtl>

مكتبة ربط مع الواجهة البرمجية لخدمة الدفع سترايب (Stripe).

## الإضافة إلى المشروع

```
اشمل "مـحا"؛
مـحا.اشمل_ملف("Alusus/Stripe"، "سـترايب.أسس")؛
```

<div dir=ltr>

```
import "Apm";
Apm.importFile("Alusus/Stripe");
```

</div>

## مثال

```
اشمل "مـحا"؛
مـحا.اشمل_ملف("Alusus/Stripe"، "سـترايب.أسس")؛
استخدم سـترايب؛

// أنشئ الوكيل
عرف وكيل: سـترايب.وكـيل(نـص("مفتاح_الواجهة_البرمجية"))؛

// متغير لحمل معلومات الرصيد.
عرف الرصيد: مـصفوفة[سـندنا[رصـيد]]؛
// هات الرصيد.;
الرصيد = وكيل.هات_الرصيد()؛

// اطبع مصفوفة الرصيد.
عرف ع: صـحيح؛
لكل ع = 0, ع < الرصيد.هات_الطول(), ع++ {
    طـرفية.اطبع(
        "النوع: %s\جالعملة: %s\جالمبلغ: %f\جالمصدر:\ج"،
        الرصيد(ع).نوع_الرصيد.صوان, الرصيد(ع).العملة.صوان, الرصيد(ع).المبلغ
    )؛
    عرف م: صـحيح؛
    لكل م = 0, م < الرصيد(ع).نوع_المصدر.هات_الطول(), م++ {
        طـرفية.اطبع(
            "    نوع المصدر: %s\ج"
            "    المبلغ: %f\ج"،
            الرصيد(ع).نوع_المصدر(م).نوع_المصدر.صوان, الرصيد(ع).نوع_المصدر(م).المبلغ
        )
    }
    طـرفية.اطبع("\ج")؛
}
```

<div dir=ltr>

```
import "Apm";
Apm.importFile("Alusus/Stripe");
use Stripe;

// Inistantiate the client.
def client: Stripe.Client(String("my_test_key"));

// Variable to hold all the balance of stripe account. 
def balanceArray : Array[SrdRef[Balance]];
// Get the balance. 
balanceArray = client.getBalance();

// Print the balance array.
def j: Int;
for j = 0, j < balanceArray.getLength(), j++ {
    Console.print(
        "type: %s\ncurrency: %s\namount: %f\ndetailed source:\n",
        balanceArray(j).balanceType.buf, balanceArray(j).currency.buf, balanceArray(j).amount
    );
    def i: Int;
    for i = 0, i < balanceArray(j).sources.getLength(), i++ {
        Console.print(
            "\tsource type: %s\n\tsource amount: %f\n",
            balanceArray(j).sources(i).sourceType.buf, balanceArray(j).sources(i).amount
        )
    }
    Console.print("\n");
}
```

</div>

## الأصناف

### زبـون (Customer) 

يحمل هذا الصنف بيانات الزبون المجلوبة من سترايب.

```
صنف زبـون {
    عرف المعرف: نـص؛
    عرف العنوان: سـندنا[عـنوان]؛
    عرف الرصيد: عـائم = 0؛
    عرف معرف_المصدر_المبدئي: نـص؛
    عرف مقصر: ثـنائي؛
    عرف زمن_الإنشاء: صـحيح[64]؛
    عرف البريد_الإلكتروني: نـص؛
    عرف بادئة_الفاتورة: نـص؛
    عرف النسق_المفضلة: مـصفوفة[نـص]؛
    عرف الاسم: نـص؛
    عرف رقم_الهاتف: نـص؛
    عرف الشحن: نـص؛
    عرف معفي_من_الضريبة: نـص؛
    عرف ساعة_اختبار: نـص؛
    عرف تسلسل_الفاتورة_التالي: صـحيح؛
    عرف العملة: نـص؛
    عرف الوصف: نـص؛
    عرف طريقة_الدفع_المبدئية: نـص؛

    عملية هذا~هيئ();

    عملية هذا~هيئ(المعرف: نـص, البريد_الإلكتروني: نـص, الاسم: نـص, النسق_المفضلة: مـصفوفة[نـص])؛

    عملية هذا~هيئ(
        المعرف: نـص، العنوان: سـندنا[عـنوان]، الرصيد: عـائم، زمن_الإنشاء: صـحيح[64]،
        العملة: نـص: معرف_المصدر_المبدئي: نـص، مقصر: ثـنائي،
        الوصف: نـص، البريد_الإلكتروني: نـص، بادئة_الفاتورة: نـص، الاسم: نـص،
        تسلسل_الفاتورة_التالي: نـص، رقم_الهاتف: نـص، النسق_المفضلة: مـصفوفة[نـص]،
        الشحن: نـص، معفي_من_الضريبة: نـص، ساعة_اختبار: نـص، طريقة_الدفع_المبدئية: نـص
    )؛
}
```

<div dir=ltr>

```
class Customer {
    def id: String;
    def address: SrdRef[Address];
    def balance: Float = 0;
    def defaultSourceId: String;
    def delinquent: Bool;
    def created: Int[64];
    def email: String;
    def invoicePrefix: String;
    def preferredLocales: Array[String];
    def name: String;
    def phone: String;
    def shipping: String;
    def taxExempt: String;
    def testClock: String;
    def nextInvoiceSequence: Int;
    def currency: String;
    def description: String;
    def defaultPaymentMethod: String;

    handler this~init();

    handler this~init(id: String, email: String, name: String, preferredLocales: Array[String]);

    handler this~init(
        id: String, address: SrdRef[Address], balance: Float, created: Int[64],
        currency: String, defaultSourceId: String, delinquent: Bool,
        description: String, email: String, invoicePrefix: String, name: String,
        nextInvoiceSequence: Int, phone: String, preferredLocales: Array[String],
        shipping: String, taxExempt: String, testClock: String, defaultPaymentMethod: String
    );
}
```

</div>

### عـنوان (Address)

يحمل بيانات عنوان بريدي.

```
صنف عـنوان {
    عرف المدينة: نـص؛
    عرف الدولة: نـص؛
    عرف السطر1: نـص؛
    عرف السطر2: نـص؛
    عرف الرمز_البريدي: نـص؛
    عرف الولاية: نـص؛

    عملية هذا~هيئ()؛
    
    عملية هذا~هيئ(المدينة: نـص، الدولة: نـص، سطر1: نـص، سطر2: نـص، الرمز_البريدي: نـص، الولاية: نـص)؛
}
```

<div dir=ltr>

```
class Address {
    def city: String;
    def country: String;
    def line1: String;
    def line2: String;
    def postalCode: String;
    def state: String;

    handler this~init();

    handler this~init(city: String, country: String, line1: String, line2: String, postalCode: String, state: String);
}
```

</div>

### رصـيد (Balance)

يحمل بيانات الرصيد الحالي.

```
صنف رصـيد {
    عرف المبلغ: عـائم = 0؛
    عرف العملة: نـص = "usd"؛
    عرف المصادر: مـصفوفة[سـندنا[مـصدر]]؛
    عرف نوع_الرصيد: نـص؛
    
    عملية هذا~هيئ()؛
    
    عملية هذا~هيئ(المبلغ: عـائم، العملة: نـص، المصادر: مـصفوفة[سـندنا[مـصدر]]، نوع_الرصيد: نـص)؛
}
```

<div dir=ltr>

```
class Balance {
    def amount: Float = 0;
    def currency: String = "usd";
    def sources: Array[SrdRef[Source]];
    def balanceType: String;

    handler this~init() {
    }

    handler this~init(amount: Float, currency: String, sources: Array[SrdRef[Source]], balanceType: String);
}
```

</div>

`المصادر` (`sources`) المصادر المساهمة في هذا الرصيد (حساب مصرفي bank_account أو بطاقة card).

`نوع_الرصيد` `balanceType` نوع هذا الرصيد (available, pending).

### عـملية_رصيد (BalanceTransaction)

يحتوي على خصائص عملية رصيد واحدة.

```
صنف عـملية_رصيد {
    عرف المعرف: نـص؛
    عرف المبلغ: عـائم = 0؛
    عرف زمن_التوفر: صـحيح[64]؛
    عرف الإنشاء: صـحيح؛
    عرف العملة: نـص = "usd"؛
    عرف الوصف: نـص؛
    عرف سعر_الصرف: عـائم؛
    عرف الرسوم: عـائم؛
    عرف تفاصيل_الرسوم: مـصفوفة[نـص]؛
    عرف المبلغ_الكلي: عـائم = 0؛
    عرف فئة_التبليغ: نـص؛
    عرف المصدر: نـص؛
    عرف الحالة: نـص؛
    عرف نوع_المصدر: نـص؛
    
    عملية هذا~هيئ()؛

    عملية هذا~هيئ(
        المعرف: نـص، المبلغ: عـائم، زمن_التوفر: صـحيح[64]، زمن_الإنشاء: صـحيح[64]،
        العملة: نـص، الوصف: نـص، سعر_الصرف: عـائم، الرسوم: عـائم،
        تفاصيل_الرسوم: مـصفوفة[نـص]، المبلغ_الكلي: عـائم، فئة_التبليغ: نـص،
        المصدر: نـص، الحالة: نـص، نوع_المصدر: نـص
    )؛
}
```

<div dir=ltr>

```
class BalanceTransaction {
    def id: String;
    def amount: Float = 0;
    def availableOn: Int[64];
    def created: Int[64];
    def currency: String = "usd";
    def description: String;
    def exchangeRate: Float;
    def fee: Float;
    def feeDetails: Array[String];
    def net: Float = 0;
    def reportingCategory: String;
    def source: String;
    def status: String;
    def sourceType: String;


    handler this~init();

    handler this~init(
        id: String, amount: Float, availableOn: Int[64], created: Int[64],
        currency: String, description: String, exchangeRate: Float, fee: Float,
        feeDetails: Array[String], net: Float, reportingCategory: String,
        source: String, status: String, sourceType: String
    );
}
```

</div>

`المعرف` (`id`) معرف قيد العملية في سترايب.

`المبلغ` (`amount`) مبلغ العملية.

`زمن_التوفر` (`availableOn`) الزمن الذي ستكون فيه القيمة متوفرة في الحساب.

`الرسوم` (`fee`) رسوم العملية.

`سعر_الصرف` (`exchangeRate`) سعر الصرف المتبع في العملية.

### تـفاصيل_فوترة (BillingDetails)

يحمل فاصيل الفوترة لزبون.

```
صنف تـفاصيل_فوترة {
    عرف العنوان: سـندنا[عـنوان]؛
    عرف البريد_الإلكتروني: نـص؛
    عرف الاسم: نـص؛
    عرف رقم_الهاتف: نـص؛
    
    عملية هذا~هيئ()؛
    
    عملية هذا~هيئ(
        عنوان: سـندنا[عـنوان]، البريد_الإلكتروني: نـص، الاسم: نـص، رقم_الهاتف: نـص
    )؛
}
```

<div dir=ltr>

```
class BillingDetails {
    def address: SrdRef[Address];
    def email: String;
    def name: String;
    def phone: String;

    handler this~init();

    handler this~init(
        address: SrdRef[Address], email: String, name: String, phone: String
    );
}
```

</div>

### جـلسة_شراء (CheckoutSession)

يحمل خصائص عملية إتمام شراء واحدة.

```
صنف جـلسة_شراء {
    عرف المعرف: نـص؛
    عرف رابط_الإلغاء: نـص؛
    عرف المعرف_الفريد: نـص؛
    عرف العملة: نـص = "usd"؛
    عرف معرف_الزبون: نـص؛
    عرف العناصر: نـص؛
    عرف النمط: نـص؛
    عرف حالة_الدفع: نـص؛
    عرف الحالة: نـص؛
    عرف رابط_النجاح: نـص؛
    عرف الرابط: نـص؛
    عرف المبلغ_الكلي: نـص؛
    
    عملية هذا~هيئ()؛
    
    عملية هذا~هيئ(
        المعرف: نـص، المعرف_الفريد: نـص، رابط_الإلغاء: نـص، رابط_النجاح: نـص، الرابط: نـص،
        العملة: نـص، معرف_الزبون: نـص، العناصر: نـص، النمط: نـص، حالة_الدفع: نـص،
        الحالة: نـص، المبلغ_الكلي: نـص
    )؛
}
```

<div dir=ltr>

```
class CheckoutSession {
    def id: String;
    def cancelUrl: String;
    def uniqeId: String;
    def currency: String = "usd";
    def customerId: String;
    def lineItems: String;
    def mode: String;
    def paymentStatus: String;
    def status: String;
    def successUrl: String;
    def url: String;
    def amountTotal: String;

    handler this~init();

    handler this~init(
        id: String, uniqeId: String, cancelUrl: String, successUrl: String, url: String,
        currency: String, customerId: String, lineItems: String,
        mode: String, paymentStatus: String, status: String, amountTotal: String
    );
}
```

</div>

`المعرف` (`id`) معرف قيد إتمام الشراء في سترايب.

`المبلغ_الكلي` (`amountTotal`) المبلغ الكلي لعملية الشراء.

`الرابط` (`url`) رابط إتمام عملية الشراء.

`رابط_النجاح` (`successUrl`) الرابط الذي يُرسل المستخدم إليه في حال نجاح العملية.

`رابط_الإلغاء` (`cancelUrl`) الرابط الذي يُرسل المستخدم إليه في حال إلغاء العملية.

### طـريقة_دفع (PaymentMethod)

يحمل معلومات لطريقة دفع واحدة.

```
صنف طـريقة_دفع {
    عرف المعرف: نـص؛
    عرف تفاصيل_الفوترة: سـندنا[تـفاصيل_فوترة]؛
    عرف تاريخ_الإنشاء: صـحيح[64]؛
    عرف العملة: نـص = "usd"؛
    عرف معرف_الزبون: نـص؛
    عرف سنة_انقضاء_الصلاحية: صـحيح؛
    عرف شهر_انقضاء_الصلاحية: صـحيح؛
    عرف آخر4: نـص؛
    عرف النوع: نـص؛
    
    عملية هذا~هيئ()؛
    
    عملية هذا~هيئ(
        المعرف: نـص، تفاصيل_الفوترة: سـندنا[تـفاصيل_فوترة]، تاريخ_الإنشاء: صـحيح[64]، سنة_انقضاء_الصلاحية: صـحيح،
        شهر_انقضاء_الصلاحية: صـحيح، العملة: نـص، آخر4: نـص، النوع: نـص
    )؛
}
```

<div dir=ltr>

```
class PaymentMethod {
    def id: String;
    def billingDetails: SrdRef[BillingDetails];
    def created: Int[64];
    def currency: String = "usd";
    def customerId: String;
    def expYear: Int;
    def expMonth: Int;
    def last4: String;
    def type: String;

    handler this~init();

    handler this~init(
        id: String, billingDetails: SrdRef[BillingDetails], created: Int[64], expYear: Int, expMonth: Int,
        currency: String, last4: String, type: String
    );
}
```

</div>

### مـصدر (Source)

يحمل معلومات لمصدر واحد من مصادر الرصيد (مثل بطاقة أو حساب مصرفي).

```
صنف مـصدر {
    عرف المبلغ: عـائم = 0؛
    عرف النوع: نـص = "card"؛
    
    عملية هذا~هيئ()؛
    
    عملية هذا~هيئ(المبلغ: عـائم، نوع_المصدر: نـص)؛
}
```

<div dir=ltr>

```
class Source {
    def amount: Float = 0;
    def sourceType: String = "card"; // "card" or "bank_account"

    handler this~init();

    handler this~init(amount: Float, sourceType: String);
}
```

</div>

### اشـتراك (Subscription)

يحمل خصائص اشتراك واحد.

```
صنف اشـتراك {
    عرف المعرف: نـص؛
    عرف معرف_التطبيق: نـص؛
    عرف ضريبة_تلقائية: ثنائي؛
    عرف زمن_بدء_دورة_الفاتورة: صـحيح[64]؛
    عرف زمن_الإنشاء: صـحيح[64]؛
    عرف زمن_البدء: صـحيح[64]؛
    عرف زمن_بدء_الفترة_الحالية: صـحيح[64]؛
    عرف زمن_انتهاء_الفترة_الحالية: صـحيح[64]؛
    عرف الإلغاء_عند_انتهاء_الاشتراك: ثنائي؛
    عرف الوصف: نـص؛
    عرف الحالة: نـص؛
    عرف زمن_انتهاء_الفترة_التجريبية: صـحيح[64]؛
    عرف العملة: نـص؛
    عرف معرف_الزبون: نـص؛
    عرف طريقة_الجمع: نـص؛
    عرف بيانات_وصفية: تـطبيق[نـص، نـص]؛
    
    عملية هذا~هيئ()؛
    
    عملية هذا~هيئ(
        المعرف: نـص، ضريبة_تلقائية: ثنائي، زمن_بدء_دورة_الفاتورة: صـحيح[64]، زمن_الإنشاء: صـحيح[64]، طريقة_الجمع: نـص،
        زمن_البدء: صـحيح[64]، الألغاء_عند_انتهاء_الاشتراك: ثنائي، زمن_انتهاء_الفترة_الحالية: صـحيح[64]،
         زمن_بدء_الفترة_الحالية: صـحيح[64]، الوصف: نـص، الحالة: نـص، زمن_انتهاء_الفترة_التجريبية: صـحيح[64]،
          معرف_الزبون: نـص، العملة: نـص، بيانات_وصفية: تـطبيق[نـص، نـص]
    )؛
}
```

<div dir=ltr>

```
class Subscription {
    def id: String;
    def application: String;
    def automaticTax: Bool;
    def billingCycleAnchor: Int[64];
    def created: Int[64];
    def startDate: Int[64];
    def currentPeriodStart: Int[64];
    def currentPeriodEnd: Int[64];
    def cancelAtPeriodEnd: Bool;
    def description: String;
    def status: String;
    def trialEnd: Int[64];
    def currency: String = "usd";
    def customerId: String;
    def collectionMethod: String;
    def metadata: Map[String, String];

    handler this~init();

    handler this~init(
        id: String, automaticTax: Bool, billingCycleAnchor: Int[64], created: Int[64],
        collectionMethod: String, startDate: Int[64], cancelAtPeriodEnd: Bool,
        currentPeriodEnd: Int[64], currentPeriodStart: Int[64], description: String, status: String,
        trialEnd: Int[64], customerId: String, currency: String, metadata: Map[String, String]
    );
}
```

</div>

`المعرف` (`id`) معرف قيد عملية اشتراك في سترايب.

`زمن_البدء` (`startDate`) زمن بدء الاشتراك.

`الحالة` (`status`) حالة الاشتراك.

`زمن_انتهاء_الفترة_التجريبية` (`trialEnd`) زمن انتهاء الفترة التجريبية.

`معرف_الزبون` (`customerId`) معرف الزبون الخاص بعملية الاشتراك.


### وكـيل (Client)

يحتوي هذا الصنف كل وظائف التواصل مع سترايب. يُهيأ باستخدام مفتاح الواجهة البرمجية المُقدم من سترايب (API key):

```
عملية هذا~هيئ(مفتاح: نـص)؛
```

<div dir=ltr>

```
handler this~init(key: String);
```

</div>

يحتوي على الوظائف التالية:

#### هات_الزبائن (getCustomers)

```
عملية هذا.هات_الزبائن(): لـا_مضمون[مـصفوفة[سـندنا[زبـون]]]؛
```

```
عملية هذا.هات_الزبائن(الحد_الأقصى: صـحيح): لـا_مضمون[مـصفوفة[سـندنا[زبـون]]]؛
```

```
عملية هذا.هات_الزبائن(الحد_الأقصى: صـحيح، آخر_معرف: نـص): لـا_مضمون[مـصفوفة[سـندنا[زبـون]]]؛
```

<div dir=ltr>

```
handler this.getCustomers(): Possible[Array[SrdRef[Customer]]]
```

```
handler this.getCustomers(limit: Int): Possible[Array[SrdRef[Customer]]]
```

```
handler this.getCustomers(limit: Int, startId: String): Possible[Array[SrdRef[Customer]]]
```

</div>

تُرجع جميع الزبائن.

`الحد_الأقصى` (`limit`): الحد الأقصى للقيود المطلوب جلبها.

`آخر_معرف` (`startId`): معرف القيد المطلوب جلب البيانات بدءًا مما يليه.

#### هات_زبونا (getCustomer)

```
عملية هذا.هات_زبونا(معرف: نـص): لـا_مضمون[سـندنا[زبـون]]
```

<div dir=ltr>

```
handler this.getCustomer(id: String): Possible[SrdRef[Customer]]
```

</div>

يرجع الزبون ذا المعرف المعطى.

#### أنش_زبونا (createCustomer)

```
عملية هذا.أنشئ_زبونا(معطيات: نـص): لـا_مضمون[نـص]
```

<div dir=ltr>

```
handler this.createCustomer(parameters: String): Possible[String]
```

</div>

تنشئ قيد زبون.

`معطيات` (`parameters`) معطيات الزبون بالصيغة التالية: "email=user123@example.com&name=john".

تُرجع معرف الزبون.

#### أيملك_الزبون_طريقة_دفع_مبدئية (doesCustomerHaveDefaultPaymentMethod)

```
عملية هذا.أيملك_الزبون_طريقة_دفع_مبدئية(معرف_الزبون: نـص): ثـنائي؛
```

<div dir=ltr>

```
handler this.doesCustomerHaveDefaultPaymentMethod(customerId: String): Bool;
```

</div>

ترجع 1 إن كان لدى الزبون بالمعرف المعطى طريقة دفع مبدئية.

####  أضف_طريقة_دفع_مبدئية_للزبون (addCustomerDefaultPaymentMethod)

```
عملية هذا.أضف_طريقة_دفع_مبدئية_للزبون(معرف_الزبون: نـص، معرف_طريقة_الدفع: نـص): ثـنائي؛
```

<div dir=ltr>

```
handler this.addCustomerDefaultPaymentMethod(customerId: String, paymentMethodId: String): Bool;
```

</div>

تضيف طريقة الدفع المحددة كطريقة دفع مبدئية للزبون. ترجع 1 في حال نجاح العملية.

#### هات_الرصيد (getBalance)

```
عملية هذا.هات_الرصيد(): لـا_مضمون[مـصفوفة[سـندنا[رصـيد]]]
```

<div dir=ltr>

```
handler this.getBalance(): Possible[Array[SrdRef[Balance]]]
```

</div>

تُرجع الرصيد لكل الحسابات التابعة لمفتاح الواجهة البرمجية.

#### هات_عمليات_الرصيد (getBalanceTranasactions)

```
عملية هذا.هات_عمليات_الرصيد(): لـا_مضمون[مـصفوفة[سـندنا[عـملية_رصيد]]]؛
```

```
عملية هذا.هات_عمليات_الرصيد(الحد_الأقصى: صـحيح): لـا_مضمون[مـصفوفة[سـندنا[عـملية_رصيد]]]؛
```

```
عملية هذا.هات_عمليات_الرصيد(الحد_الأقصى: صـحيح، آخر_معرف: نـص): لـا_مضمون[مـصفوفة[سـندنا[عـملية_رصيد]]]؛
```

<div dir=ltr>

```
handler this.getBalanceTranasactions(): Possible[Array[SrdRef[BalanceTranasaction]]];
```

```
handler this.getBalanceTranasactions(limit: Int): Possible[Array[SrdRef[BalanceTranasaction]]];
```

```
handler this.getBalanceTranasactions(limit: Int, startId: String): Possible[Array[SrdRef[BalanceTranasaction]]];
```

</div>

ترجع قائمة العمليات التي ساهمت في إيصال الحساب إلى الرصيد الحالي (مثل الدفع والتحويل وما شابه).

`الحد_الأقصى` (`limit`): الحد الأقصى للقيود المطلوب جلبها.

`آخر_معرف` (`startId`): معرف القيد المطلوب جلب البيانات بدءًا مما يليه.

#### هات_عملية_رصيد (getBalanceTranasaction)

```
عملية هذا.هات_عملية_رصيد(معرف: نـص): لـا_مضمون[سـندنا[عـملية_رصيد]]
```

<div dir=ltr>

```
handler this.getBalanceTranasaction(id: String): Possible[SrdRef[BalanceTranasaction]]
```

</div>

ترجع عملية الرصيد ذات المعرف المحدد.

#### أنشئ_جلسة_تحكم_بالفوترة (createBillingPortalSession)

```
عملية هذا.أنشئ_جلسة_تحكم_بالفوترة(معطيات: نـص): لـا_مضمون[نـص]
```

<div dir=ltr>

```
handler this.createBillingPortalSession(parameters: String): Possible[String]
```

</div>

تنشئ جلسة جديدة للتحكم بالدفع.

`معطيات` (`parameters`) معطيات الاشتراك المطلوبة بالصيغة التالية: "customer=customerID&returnUrl=returnUrl".

تُرجع رابط جلسة بوابة الدفع.

```
عملية هذا.أنشئ_جلسة_تحكم_بالفوترة(
    معرف_الزبون: نص،
    رابط_الرجوع: مـؤشر_محارف
): لـا_مضمون[نـص]
```

<div dir=ltr>

```
handler this.createBillingPortalSession(
    customerId:String, 
    returnUrl: CharsPtr
): Possible[String]
```

</div>

هذه النسخة من دالة `أنشئ_جلسة_تحكم_بالفوترة` تستلم معطيات مفصلة بدل معطى خام كما في النسخة السابقة.

`معرف_الزبون` (`customerId`): معرف قيد الزبون لفتح جلسة بوابة فاتورة خاصة به.

`رابط_الرجوع` (`returnUrl`): الرابط لاعادة توجيه الزبون اليه عند الانتهاء من بوابة الفاتورة.

تُرجع رابط جلسة التحكم بالفوترة.

#### هات_جلسات_إتمام_الشراء (getCheckoutSessions)

```
عملية هذا.هات_جلسات_إتمام_الشراء(): لـا_مضمون[مـصفوفة[سـندنا[جـلسة_شراء]]]
```

```
عملية هذا.هات_جلسات_إتمام_الشراء(الحد_الأقصى: صـحيح): لـا_مضمون[مـصفوفة[سـندنا[جـلسة_شراء]]]
```

```
عملية هذا.هات_جلسات_إتمام_الشراء(الحد_الأقصى: صـحيح، آخر_معرف: نـص): لـا_مضمون[مـصفوفة[سـندنا[جـلسة_شراء]]]
```

<div dir=ltr>

```
handler this.getCheckoutSessions(): Possible[Array[SrdRef[CheckoutSession]]]
```

```
handler this.getCheckoutSessions(limit: Int): Possible[Array[SrdRef[CheckoutSession]]]
```

```
handler this.getCheckoutSessions(limit: Int, startId: String): Possible[Array[SrdRef[CheckoutSession]]]
```

</div>

ترجع قائمة جلسات إتمام الشراء.

`الحد_الأقصى` (`limit`): الحد الأقصى للقيود المطلوب جلبها.

`آخر_معرف` (`startId`): معرف القيد المطلوب جلب البيانات بدءًا مما يليه.

#### هات_جلسة_إتمام_الشراء (getCheckoutSession)

```
عملية هذا.هات_جلسة_إتمام_الشراء(معرف_الجلسة: نـص): لـا_مضمون[سـندنا[جـلسة_شراء]]
```

<div dir=ltr>

```
handler this.getCheckoutSession(sessionId: String): Possible[SrdRef[CheckoutSession]]
```

</div>

ترجع جلسة إتمام الشراء ذات المعرف المعطى.

#### أنشئ_جلسة_إتمام_شراء (createCheckoutSession)

```
عملية هذا.أنشئ_جلسة_إتمام_شراء(معطيات: نـص): لـا_مضمون[نـص]
```

<div dir=ltr>

```
handler this.createCheckoutSession(parameters: String): Possible[String]
```

</div>

تنشئ جلسة إتمام شراء جديدة.

`معطيات` (`parameters`) معطيات الجلسة المطلوبة بالصيغة التالية: "customer=customerID&line_items=planID".

تُرجع معرف الجلسة المُنشأة.

```
عملية هذا.أنشئ_جلسة_إتمام_شراء(
    العناصر: تـطبيق[نـص، صـحيح]،
    رابط_النجاح: مـؤشر_محارف
): لـا_مضمون[نـص]؛
```

```
عملية هذا.أنشئ_جلسة_إتمام_شراء(
    العناصر: تـطبيق[نـص، صـحيح]،
    معرف_الزبون: نـص،
    رابط_النجاح: مـؤشر_محارف
): لـا_مضمون[نـص]
```

<div dir=ltr>

```
handler this.createCheckoutSession(
    items: Map[String, Int],
    successUrl: CharsPtr
): Possible[String]
```

```
handler this.createCheckoutSession(
    items: Map[String, Int],
    customerId: String,
    successUrl: CharsPtr
): Possible[String]
```

</div>

هاتان النسخنان من دالة `أنشئ_جلسة_إتمام_شراء` تستلمان معطيات مفصلة بدل معطى خام كما في النسخة السابقة.

`العناصر` (`items`): تطبيق يمثل مفتاحه معرف السعر من سترايب (price ID) بينما تمثل قيمته عدد العناصر
المطلوبة.

`معرف_الزبون` (`customerId`): معرف قيد الزبون الذي يقوم بعملية الشراء.

`رابط_النجاح` (`successUrl`): الرابط الذي سيُحول إليه المستخدم بعد نجاح عملية الشراء.

تُرجع معرف الجلسة المُنشأة.

#### هات_الاشتراكات (getSubscriptions)

```
عملية هذا.هات_الاشتراكات(): لـا_مضمون[مـصفوفة[سـندنا[اشتراك]]]
```

```
عملية هذا.هات_الاشتراكات(شرط_التصفية: نـص): لـا_مضمون[مـصفوفة[سـندنا[اشتراك]]]
```

<div dir=ltr>

```
handler this.getSubscriptions(): Possible[Array[SrdRef[Subscription]]]
```

```
handler this.getSubscriptions(filterQuery: String): Possible[Array[SrdRef[Subscription]]]
```

</div>

ترجع قائمة الاشتراكات.

`شرط_التصفية` (`filterQuery`): تركيب يحتوي الشرط الذي تُصفى به النتائج. ستجلب الدالة القيود التي
تطابق هذا الشرط دون غيرها.

#### هات_اشتراكا (getSubscription)

```
عملية هذا.هات_اشتراكا(معرف_الاشتراك: نـص): لـا_مضمون[سـندنا[اشتراك]]
```

<div dir=ltr>

```
handler this.getSubscription(sessionId: String): Possible[SrdRef[Subscription]]
```

</div>

ترجع الاشتراك ذا المعرف المعطى.

#### أنشئ_اشتراكا (createSubscription)

```
عملية هذا.أنشئ_اشتراكا(معطيات: نـص): لـا_مضمون[نـص]
```

<div dir=ltr>

```
handler this.createSubscription(parameters: String): Possible[String]
```

</div>

تنشئ اشتراكا جديدا.

`معطيات` (`parameters`) معطيات الاشتراك المطلوبة بالصيغة التالية: "customer=customerID&line_items=planID".

تُرجع معرف الاشتراك المُنشأ.

```
عملية هذا.أنشئ_اشتراكا(
    العناصر: تـطبيق[نـص، صـحيح]،
    معرف_الزبون: نص
): لـا_مضمون[نـص]
```

<div dir=ltr>

```
handler this.createSubscription(
    items: Map[String, Int],
    customerId: String
): Possible[String]
```

</div>

هذه النسخة من دالة `أنشئ_اشتراكا` تستلم متعطيات مفصلة بدل معطى خام كما في النسخة السابقة.

`العناصر` (`items`): تطبيق يمثل مفتاحه معرف السعر من سترايب (price ID) بينما تمثل قيمته عدد العناصر
المطلوبة.

`معرف_الزبون` (`customerId`): معرف قيد الزبون الذي يقوم  بالاشتراك.

تُرجع معرف الاشتراك المُنشأ.

#### حدث_اشتراكا (updateSubscription)

```
عملية هذا.حدث_اشتراكا(معرف_الاشتراك: نـص، معطيات: نـص): لـا_مضمون[نـص]؛
```

<div dir=ltr>

```
handler this.updateSubscription(subscriptionId: String, parameters: String): Possible[String];
```

</div>

تحدث الاشتراك ذا المعرف المعطى.

`معطيات` (`parameters`) معطيات الاشتراك المطلوبة بالصيغة التالية: "customer=customerID&line_items=planID".

#### هات_طرق_الدفع (getPaymentMethods)

```
عملية هذا.هات_طرق_الدفع(معرف_الزبون: نـص): لـا_مضمون[مـصفوفة[سـندنا[طـريقة_دفع]]]؛
```

<div dir=ltr>

```
handler this.getPaymentMethods(customerId: String): Possible[Array[SrdRef[PaymentMethod]]];
```

</div>

ترجع طرق الدفع التي يملكها الزبون ذو المعرف المعطى.

#### هات_طريقة_دفع (getPaymentMethod)

```
عملية هذا.هات_طريقة_دفع(معرف_طريقة_الدفع: نـص): لـا_مضمون[سـندنا[طـريقة_دفع]]؛
```

<div dir=ltr>

```
handler this.getPaymentMethod(paymentMethodId: String): Possible[SrdRef[PaymentMethod]];
```

</div>

ترجع طريقة الدفع ذات المعرف المعطى.


### أخـطاء (Errors)

الوحدة الفرعية `أخـطاء` تحتوي تعريفات لرموز الأخطاء التي يمكن لمكتبة سـترايب إرجاعها.

* `أخـطاء._غير_موثق_` (`Errors.UNAUTHENTICATED`): تُرجع عند استدعاء سترايب بمفتاح خاطئ.
* `أخـطاء._اتصال_` (`Errors.CONNECTION`): تُرجع عند فشل الاتصال بخوادم سترايب.
* `أخـطاء._غير_متوقع_` (`Errors.UNEXPECTED`): تُرجع عند استلام رد غير متوقع من سترايب.
* `أخـطاء._غير_موجود_` (`Errors.NOT_FOUND`): تُرجع عند الفشل في العثور على القيد ذي المعرف المعطى.

</div>
