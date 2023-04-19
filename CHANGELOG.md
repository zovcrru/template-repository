# Version history

We follow [Semantic Versions](https://semver.org/).


## [0.0.7] (2023-04-14)

### Fixed
- Исправлена обработка параметра DATABASE для sqlite баз данных: теперь не требует параметр DB_CONNECT
- Исправлено форматирование столбца СНИЛС (load_xls_db.format_snils): учитывает разный формат данных в одном столбце
  ('***-***-*** **','***-***-***','*********')
### Changed
- Исправлено вычисление контрольной суммы СНИЛС (load_xls_db.calculate_snils)

### Added
- Добавлено оформление заголовка выходного xlsx-файла

## [0.0.6] (2023-04-11)

### Changed
- Убран lower() у параметра FILE_NAME

### Added
- Добавлена обработка параметра SELECT: выполняет заданный в ini-файле select и записывает результат в xlsx-файл с тем же именем,
  что и обрабатываемый файл, в директорию, заданную параметром DIR_OUT

## [0.0.5] (2023-04-07)

### Changed
- Все функции для работы с параметрами вынесены в модуль utils_ini.py

## [0.0.4] (2023-04-06)

### Added
- Добавлено вычисление контрольной суммы СНИЛС (load_xls_db.calculate_snils)
- Добавлен параметр NO_CONTROL_NUMBER: вычислять или нет контрольную сумму

## [0.0.3] (2023-03-14)

### Added
- Добавлена обработка поля СНИЛС, заданного в ini-файле (SNILS) (utils_xls.read_excel).
- Добавлены функции работы с параметрами: set_parameter, set_parameter_int,set_parameter_list,
  set_parameter_reset

### Changed
- Общие переменные вынесены в файл global_vars.py
- Функция parse_config_xls перенесена в модуль utils_log.py

## [0.0.2] (2023-03-06)

### Fixed
- Изменен размер поля в CREATE TABLE (load_xls_db.read_struct_excel) с VARCHAR(32000) на VARCHAR(3200) из-за ошибки в db2:
  SQL0670N The statement failed because the row or column size of the resulting table would have exceeded the row or column size limit: "32677"
  В sqlite и postgres работает и с VARCHAR(32000).
- Убран lower() у параметров db_name и db_connect (load_xls_db.parse_config_db), т.к в db2 регистрозависимый пароль.

### Added
- Вставлена обработка списка листов, заданных в ini-файле (SHEETS) (utils_xls.read_excel).
  Если в xlsx-файле только один лист, заданный список игнорируется. Если несколько, проверяется соответствие между заданными листами и имеющимися.
