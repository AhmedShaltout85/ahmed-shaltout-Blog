### Ahmed Shaltout GitHub Blog

شرح إنشاء موقع مجاني باستضافة مجانية على GitHab Pages، وإدارة التعديل والإضافة على الموقع من خلال جهازك الشخصي، ونشر الموقع يتم بشكل تلقائي باستخدام GitHub Actions. محتوى الموقع يتم كتابته باستخدام MarkDown، وتطبيق أو أداة MkDocs تتولى عنك انشاء ملفات الموقع النهائية من HTML و CSS و javascript.
أهم الأوامر⚓︎
نسخ الموقع من على
git clone git@github.com:<userName>/<repoName>.git
إنشاء ملفات الموقع الأساسية
mkdocs new <repoName>
تجربة الموقع محليًا
mkdocs serve
إنشاء مجلد .github/workflows/
mkdir -p .github/workflows/
إنشاء ملف .github/workflows/gh-deploy.yml
nano .github/workflows/gh-deploy.yml
بالمحتوى التالي:
name: gh-deploy

on:
  push:
    branches:
      - main

jobs:
  build:
    name: MkDocs Github Pages automatic deployment
    runs-on: ubuntu-latest
    steps:
      - name: Checkout main
        uses: actions/checkout@v2

      - name: Set up Python 3.9
        uses: actions/setup-python@v2
        with:
          python-version: '3.9'

      - name: Install requirements
        run: |
          python -m pip install --upgrade pip
          pip install -r requirements.txt
      - name: MkDocs gh-deploy
        run: |
          git pull
          mkdocs gh-deploy
إنشاء ملف requirements.txt
nano requirements.txt
بالمحتوى التالي:
mkdocs>=1.2.2
إرسال ملفات الموقع إلى GitHub
git add .
git commit -m 'init'
git push
mkdocs gh-deploy
rm -r site
استخدم الأوامر التالية بالتريب بعد إجراء أي تعديل على الموقع:
git add .
git commit -m 'TEST01'
git push
مراجع
⚓︎
MkDocs
