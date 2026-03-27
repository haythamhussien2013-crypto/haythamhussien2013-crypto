import csv

results_file = "operations.csv"
output_file = "results.md"

with open(results_file, newline="", encoding="utf-8") as f:
    reader = csv.DictReader(f)
    with open(output_file, "w", encoding="utf-8") as out:
        out.write("# 📊 نتائج العمليات / الاختبارات\n\n")
        out.write("| نوع العملية | الوصف | التاريخ | الساعة | المدة |\n")
        out.write("|-------------|-------|---------|--------|-------|\n")
        for row in reader:
            out.write(f"| {row['نوع العملية']} | {row['الوصف']} | {row['التاريخ']} | {row['الساعة']} | {row['المدة']} |\n")

print("✅ تم إنشاء ملف results.md جاهز للعرض في GitHub")