import os
import datetime

def generate_readme():
    content = "# 🏅 شهاداتي وإنجازاتي\n\n"

    # قسم ملفات الشهادات داخل المستودع
    content += "## 📂 ملفات الشهادات داخل المستودع\n"
    for root, dirs, files in os.walk("."):
        for file in files:
            if file.endswith((".pdf", ".json", ".md")) and file != "README.md":
                path = os.path.join(root, file)
                timestamp = os.path.getmtime(path)
                date_str = datetime.datetime.fromtimestamp(timestamp).strftime("%Y-%m-%d %H:%M:%S")
                content += f"- {file} (آخر تحديث: {date_str})\n"

    # قسم روابط المؤسسات البحثية
    content += "\n## 🌍 روابط أهم المؤسسات والمعاهد البحثية\n"
    institutes = [
        {"name": "MIT - Massachusetts Institute of Technology", "link": "https://www.mit.edu/"},
        {"name": "XPRIZE Foundation", "link": "https://www.xprize.org/"},
        {"name": "WIPO - World Intellectual Property Organization", "link": "https://www.wipo.int/"},
        {"name": "Harvard University", "link": "https://www.harvard.edu/"},
        {"name": "Stanford University", "link": "https://www.stanford.edu/"},
        {"name": "Oxford University", "link": "https://www.ox.ac.uk/"},
        {"name": "Cambridge University", "link": "https://www.cam.ac.uk/"},
        {"name": "Caltech", "link": "https://www.caltech.edu/"},
        {"name": "Max Planck Society", "link": "https://www.mpg.de/en"},
        {"name": "CNRS - French National Centre for Scientific Research", "link": "https://www.cnrs.fr/en"},
        {"name": "Tokyo University", "link": "https://www.u-tokyo.ac.jp/en/"},
        {"name": "ETH Zurich", "link": "https://ethz.ch/en.html"},
        {"name": "Carnegie Mellon University", "link": "https://www.cmu.edu/"},
        {"name": "Princeton University", "link": "https://www.princeton.edu/"},
        {"name": "Yale University", "link": "https://www.yale.edu/"},
        {"name": "UC Berkeley", "link": "https://www.berkeley.edu/"},
        {"name": "Imperial College London", "link": "https://www.imperial.ac.uk/"},
        {"name": "National University of Singapore", "link": "https://nus.edu.sg/"},
        {"name": "Tsinghua University", "link": "https://www.tsinghua.edu.cn/en/"},
        {"name": "Peking University", "link": "https://english.pku.edu.cn/"}
    ]
    for inst in institutes:
        content += f"- [{inst['name']}]({inst['link']})\n"

    # قسم الذكاء الاصطناعي والـ Quantum
    content += "\n## 🤖 الذكاء الاصطناعي والـ Quantum Computing\n"
    ai_quantum = [
        {"name": "IBM Quantum", "link": "https://www.ibm.com/quantum"},
        {"name": "Google Quantum AI", "link": "https://quantumai.google/"},
        {"name": "Microsoft Quantum", "link": "https://azure.microsoft.com/en-us/solutions/quantum-computing/"},
        {"name": "Quantum Computing at MIT", "link": "https://quantum.mit.edu/"},
        {"name": "Quantum Flagship (EU)", "link": "https://qt.eu/"},
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