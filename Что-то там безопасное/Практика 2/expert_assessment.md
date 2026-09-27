# Экспертная оценка безопасности

## Сводка найденных уязвимостей

| Язык | Тип | CWE | OWASP | CVSS | Критичность |
|------|-----|-----|-------|------|-------------|
| Python | SQL Injection | CWE-89 | A03 | 9.8 | Critical |
| Python | Stored XSS | CWE-79 | A03 | 8.2 | High |
| C++ | Buffer Overflow | CWE-120 | A06 | 9.5 | Critical |
| C++ | Command Injection | CWE-78 | A03 | 9.8 | Critical |
| C++ | Format String | CWE-134 | A03 | 7.8 | High |
| JavaScript | SQL Injection | CWE-89 | A03 | 9.8 | Critical |
| JavaScript | XSS | CWE-79 | A03 | 8.2 | High |
| JavaScript | Command Injection | CWE-78 | A03 | 9.8 | Critical |

## Ключевые выводы

1. **XSS (CWE-79)** — 1-е место в CWE Top 25 2025 [citation:4]
2. **SQL Injection (CWE-89)** — 2-е место, поднялась на одну позицию [citation:4]
3. **Buffer Overflow (CWE-120)** — впервые в Top 25 2025 (11-е место) [citation:4]
4. **Command Injection (CWE-78)** — 9-е место, 20 CVE в CISA KEV [citation:4]

## Рекомендации

1. **Python:** параметризованные запросы, убрать `|safe`
2. **C++:** `strncpy`/`std::string`, избегать `system()`, фиксированные строки формата
3. **JavaScript:** параметризованные запросы, `execFile` вместо `exec`, экранирование вывода
---