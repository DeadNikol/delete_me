# Вторая практика
## Шаг первый
### Приложение 1: python проект
Для запуска выполнить:
```
pip install flask
python3 vulnmart/app.py
```

Для его `Sast` проверки будет использоваться bandit
```shell
pip install bandit
bandit -r <file_path.py>
```

Для `Dast` проверки будет использоваться OWASP ZAP  
1. Необходимо убедитсья, что приложение запущено
2. Запустить ZAP через docker

```docker
docker run --rm -v $(pwd):/zap/wrk/:rw \
  ghcr.io/zaproxy/zaproxy:stable zap-full-scan.py \
  -t http://host.docker.internal:5055 \
  -r zap_full_report.html
```
> - zap-full-scan.py включает активные атаки (XSS, SQLi и др.) .
> - -t — целевой URL. Обратите внимание: если вы используете Docker на Windows/Mac, для доступа к приложению на хосте из контейнера нужно использовать host.docker.internal.
> - -r — файл для отчета.
3. ZAP выплюнет html отчёт
 

### Приложение 2: C++ проект
Для запуска запустить в `bash`:
```bash
g++ -Wall -Wextra -g -std=c++17 -o vulnerable vulnerable.cpp
./vulnerable "test_input"
```

Для его проверки будет использоваться cppcheck (Sast) (Ставить в Linux)
```bash
sudo apt install cppcheck
cppcheck --enable=all --inconclusive <file_path.cpp>
```

### Приложение 3: JavaScript проект
Для запуска нужно установить node.js и после этого уже запустить в том же `bash`
```bash
sudo apt install nodejs npm -y
npm install express sqlite3
node vulnerable.js
```

ДЛя проверки будет использоваться ESLint (Sast)
```bash
npm install --save-dev eslint eslint-plugin-security

touch .eslintrc.json
{
  "plugins": ["security"],
  "extends": ["plugin:security/recommended"]
}

npx eslint vulnerable.js
```

## Шаг второй
### CWE — Классификация слабостей
CWE (Common Weakness Enumeration) — это стандартизированный список типов слабостей программного и аппаратного обеспечения, поддерживаемый MITRE . CWE описывает классы дефектов (например, «SQL-инъекция», «переполнение буфера»), а не конкретные экземпляры.

**Ключевое различие CWE и CVE:**
-	`CVE` отвечает на вопрос: «Какая конкретная уязвимость существует в этом конкретном продукте и версии?»
-	`CWE` отвечает на вопрос: «Какая это категория ошибки кодирования или проектирования?» 

Одному `CWE` может соответствовать тысячи `CVE`. Например, `CWE-79` (XSS) охватывает тысячи конкретных `CVE` в разных приложениях.

### CVE — Конкретные уязвимости
`CVE` (Common Vulnerabilities and Exposures) — программа, управляемая MITRE при спонсорстве CISA, присваивающая уникальные идентификаторы каждой публично раскрытой уязвимости . Формат: CVE-YYYY-NNNN.

### CVSS — Оценка серьёзности
`CVSS` (Common Vulnerability Scoring System) — стандартизированная числовая оценка серьёзности уязвимости от 0 до 10, разработанная FIRST . Учитывает вектор атаки, сложность, требуемые привилегии, взаимодействие с пользователем и влияние на конфиденциальность, целостность и доступность .

### OWASP Top 10 — Категории рисков
| Категория | Описание |
|-----------|----------|
| A01: Broken Access Control | Сбой механизмов контроля доступа |
| A02: Cryptographic Failures | Ошибки в криптографии |
| A03: Injection | Инъекции (SQL, XSS, Command, XPath) |
| A04: Insecure Design | Небезопасный дизайн |
| A05: Security Misconfiguration | Недостатки конфигурации |
| A06: Vulnerable Components | Уязвимые и устаревшие компоненты |
| A07: Authentication Failures | Ошибки аутентификации |
| A08: Integrity Failures | Ошибки целостности ПО и данных |
| A09: Logging Failures | Ошибки логирования и мониторинга |
| A10: SSRF | Подделка запросов на стороне сервера |


## Шаг третий
### Проверка Sast через bandit
```
pip install bandit
bandit -r vulnmart/app.py
```


