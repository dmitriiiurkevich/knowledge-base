Современный браузер — это очень сложное приложение, выполнение которого распараллеливается на множество независимо выполняющихся процессов. И нет никакой единой спецификации, которая бы регламентировала структуру и особенности взаимодействия этих процессов.

*Chrome* essential architecture:
- Browser process
	- UI thread — поток пользовательского интерфейса
	- network thread — сетевой поток
	- storage thread
	- ...
- Render process
	- multiple processes assigned 
		- until recently: to each tab 
		- now: each site and each cross-site iframe separately
- GPU process
- Utility process
- Plugin process

Все вышеперечисленные компоненты браузера могут запускаться как отдельные сервисы, если браузер располагает достаточным объёмом необходимых ресурсов, а могут быть агрегированы в единый процесс.

## Per-frame renderer processes - Site Isolation
межсайтовый iframe
https://habr.com/ru/articles/511318/



