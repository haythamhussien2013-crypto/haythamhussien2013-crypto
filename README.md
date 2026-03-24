import os
import datetime

def generate_readme():
    content = "# 🏅 شهاداتي وإنجازاتي\n\n"

    # توقيت العملية
    run_time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

    # قراءة حالة العملية من متغيرات GitHub Actions
    workflow_name = os.getenv("GITHUB_WORKFLOW", "Unknown Workflow")
    run_id = os.getenv("GITHUB_RUN_ID", "N/A")
    run_number = os.getenv("GITHUB_RUN_NUMBER", "N/A")
    job_status = os.getenv("JOB_STATUS", "success")  # لازم يتحدد من الـ job نفسه

    # نسبة النجاح الحقيقية
    success_rate = "100%" if job_status.lower() == "success" else "0%"

    content += f"**⏱️ وقت آخر تحديث:** {run_time}\n"
    content += f"**⚙️ العملية:** {workflow_name} (Run #{run_number}, ID: {run_id})\n"
    content += f"**✅ نسبة نجاح العملية:** {success_rate}\n\n"

    # قسم ملفات الشهادات داخل المستودع
    content += "## 📂 ملفات الشهادات داخل المستودع\n"

    files_list = []
    for root, dirs, files in os.walk("."):
        for file in files:
            if file.endswith((".pdf", ".json", ".md")) and file != "README.md":
                path = os.path.join(root, file)
                timestamp = os.path.getmtime(path)
                files_list.append((file, path, timestamp))

    # ترتيب الملفات حسب التاريخ (الأحدث أولًا)
    files_list.sort(key=lambda x: x[2], reverse=True)

    for file, path, timestamp in files_list:
        date_str = datetime.datetime.fromtimestamp(timestamp).strftime("%Y-%m-%d %H:%M:%S")
        github_link = f"https://github.com/USERNAME/REPO_NAME/blob/main/{path}"
        content += f"- [{file}]({github_link}) (آخر تحديث: {date_str})\n"

    # قسم المؤسسات البحثية
    content += "\n## 🌍 روابط أهم المؤسسات والمعاهد البحثية\n"
    institutes = [
        {"name": "MIT - Massachusetts Institute of Technology", "link": "https://www.mit.edu/"},
        {"name": "XPRIZE Foundation", "link": "https://www.xprize.org/"},
        {"name": "WIPO - World Intellectual Property Organization", "link": "https://www.wipo.int/"},
        {"name": "Harvard University", "link": "https://www.harvard.edu/"},
        {"name": "Stanford University", "link": "https://www.stanford.edu/"}
    ]
    for inst in institutes:
        content += f"- [{inst['name']}]({inst['link']})\n"

    # قسم الذكاء الاصطناعي والـ Quantum
    content += "\n## 🤖 الذكاء الاصطناعي والـ Quantum Computing\n"
    ai_quantum = [
        {"name": "IBM Quantum", "link": "https://www.ibm.com/quantum-computing/"},
        {"name": "Google Quantum AI", "link": "https://quantumai.google/"},
        {"name": "Microsoft Quantum", "link": "https://azure.microsoft.com/en-us/services/quantum/"},
        {"name": "OpenAI", "link": "https://openai.com/"},
        {"name": "DeepMind", "link": "https://deepmind.com/"}
    ]
    for org in ai_quantum:
        content += f"- [{org['name']}]({org['link']})\n"

    # كتابة الملف README
    with open("README.md", "w", encoding="utf-8") as f:
        f.write(content)

if __name__ == "__main__":
    generate_readme()