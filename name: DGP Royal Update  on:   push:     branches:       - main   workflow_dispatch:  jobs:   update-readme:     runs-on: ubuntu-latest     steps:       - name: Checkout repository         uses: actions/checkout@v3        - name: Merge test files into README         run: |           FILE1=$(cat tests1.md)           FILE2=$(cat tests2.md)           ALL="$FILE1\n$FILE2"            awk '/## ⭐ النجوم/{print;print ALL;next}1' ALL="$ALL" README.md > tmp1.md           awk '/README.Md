import requests
import subprocess

# إعدادات عامة
owner = "haythamhussien2013-crypto"
repo = "crypto"
token = "YOUR_GITHUB_TOKEN"
headers = {"Authorization": f"token {token}"}

# 1. جلب أرقام التجارب
def get_runs():
    url = f"https://api.github.com/repos/{owner}/{repo}/actions/runs"
    response = requests.get(url, headers=headers)
    return response.json()["workflow_runs"]

# 2. جلب الألقاب والكؤوس (Artifacts)
def get_artifacts():
    url = f"https://api.github.com/repos/{owner}/{repo}/actions/artifacts"
    response = requests.get(url, headers=headers)
    return response.json()["artifacts"]

# 3. قراءة نص رسمي من README
def read_readme(file_path="README.md"):
    with open(file_path, "r", encoding="utf-8") as f:
        return f.read()

# 4. توقيع بالمفتاح الخاص (OpenSSL)
def sign_message(message, private_key="private.pem"):
    with open("message.txt", "w", encoding="utf-8") as f:
        f.write(message)
    subprocess.run(["openssl", "dgst", "-sha256", "-sign", private_key, "-out", "signature.bin", "message.txt"])
    return "signature.bin"

# دمج النتائج
print("=== ملف المفاجأة السيادي ===\n")

print("🔢 أرقام التجارب:")
for run in get_runs():
    print(f"- رقم: {run['run_number']} | الحالة: {run['conclusion']} | التاريخ: {run['created_at']}")

print("\n🏆 الألقاب والكؤوس:")
for artifact in get_artifacts():
    print(f"- لقب/كأس: {artifact['name']} | رقم: {artifact['id']} | حجم: {artifact['size_in_bytes']} بايت")

print("\n📜 نص رسمي من README:")
readme_text = read_readme()
print(readme_text[:300], "...")  # عرض أول 300 حرف كعينة

print("\n🔑 توقيع رسمي:")
signature_file = sign_message("DGP Sovereign Record 2026")
print(f"تم إنشاء توقيع في الملف: {signature_file}")