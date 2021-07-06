Небольшой логгер, позволяющий создавать сообщения о ходе работы программы. Логгер пишет время сообщений. В функции main приведен пример использования логгера.

Как пользоваться логгером.
LOGGER::Logger* logger = LOGGER::Logger::GetInstance(); - получить указатель на логгер
logger->WriteLog(LOGGER::LogLevel::Error, "Not enough arguments"); - пример записи в лог

Второй аргумент - что пишем в лог, первый аргумент может быть:
LOGGER::LogLevel::Info     - просто информация, строка запишется в файл.
LOGGER::LogLevel::Debug    - строка запишется в файл и будет выведена в консоль. Используйте для отладки в консоли.
LOGGER::LogLevel::Warning  - предупреждение, строка запишется в файл и будет выведена в консоль. Используйте для
 предупреждения пользователя.
LOGGER::LogLevel::Error    - ошибка, строка запишется в файл, выведется в консоль, сработает assert, программа
 завершит работу, если сборка дебажная.

КАК ИЗМЕРЯТЬ ВРЕМЯ С ПОМОЩЬЮ ЛОГГЕРА
logger->ResetTimer();                                           - сбросить таймер
logger->GetTime("Time of adding operation", true);    - метод GetTime отмеряет и выводит в логфайл время от прошлого вызова GetTime
или ResetTimer (GetTime тоже обнуляет таймер, если Вы измеряете время на соседних участках кода, использовать ResetTimer не нужно).

У метода GetTime 3 параметра, все со значениями по умолчанию:
1) std::string message - сообщение, которое будет выведено перед значением времени. Используйте это для того, чтобы обозначить на каком
участке кода считалось время (например "Time of algorithm1"). Значение по умолчанию - пустая строка.
2) bool writeToConsole - передайте вторым параметром true, чтобы время также вывелось в консоль. По умолчанию значение false.
3) int unit - единица измерения времени, передайте третьим параметром 1, чтобы измерять в секундах, 0 чтобы измерять в мс. Знач. по умол. 0.


Логи хранятся в файле Logfile.txt.
logger->ShowLog();    - вывести логи в консоль.
При новом запуске программы предыдущие логи сохраняются.
Чтобы очистить логфайл, вызовите метод logger->ClearLogFile()
