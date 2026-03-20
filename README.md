

library(dplyr)
library(readr)
library(lubridate)

# قراءة ملف النتائج
results <- read_csv("test_results.csv")

# استخراج المستحقات التقنية
entitlements <- results %>%
  filter(Test_Type == "Technical") %>%      # اختبارات تقنية فقط
  mutate(Date = ymd(Date)) %>%              # تحويل التاريخ
  group_by(Employee_ID) %>%                 # تجميع حسب الشخص
  summarise(
    total_tests = n(),                      # عدد الاختبارات
    passed = sum(Result == "Passed"),       # عدد الاختبارات الناجحة
    failed = sum(Result == "Failed"),       # عدد الاختبارات الفاشلة
    entitlement_points = sum(Points),       # مجموع النقاط
    last_test = max(Date)                   # آخر اختبار
  )

print(entitlements)## Hi there 👋

<!--
**haythamhussien2013-crypto/haythamhussien2013-crypto** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
