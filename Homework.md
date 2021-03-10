# HOMEWORK01_Alferov_IU8-22




1. Скачайте библиотеку boost с помощью утилиты wget. Адрес для скачивания https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz. 
```
  $ wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz 
```
2. Разархивируйте скаченный файл в директорию ~/boost_1_69_0
```
   $ mkdir ~/boost_1_69_0  // mkdir создаёт папку
   $ tar -C ~/boost_1_69_0 –xzf boost_1_69_0.tar.gz // tar разархивирует (ключ -x) архив в аудиторию ~/boost_1_69_0 (об этом говорит ключ -C), архив сжат (.gz) поэтому дополнительно используем ключ -z -f - выводит результат в файл или на устройство
```
3. Подсчитайте количество файлов в директории ~/boost_1_69_0 не включая вложенные директории.
```
   $ find ./ -maxdepth 1 -type f | wc -l //find - команда для поиска в данном каталоге (./), без поиска в подкаталогах (параметр -maxdepth 1) всех файлов (-type f). Затем результат выполнения первой команды направляется в команду wc (wordcounter) и выводит количество строк (параметр -l)
Ответ:12
```
4. Подсчитайте количество файлов в директории ~/boost_1_69_0 включая вложенные директории.
```
   $ find ./ -type f | wc -l
Ответ: 61192
```
5. Подсчитайте количество заголовочных файлов, файлов с расширением .cpp, сколько остальных файлов (не заголовочных и не .cpp).
```
  $ find . -type f -name "*.h" | wc -l //поиск и подсчёт файлов с расширением .h
Количетсво заголовочных файлов: 296 
  $ find . -type f -name "*.cpp" | wc -l
Количество файлов .cpp: 13774
  $ find . -type f\(! -name "*.h" ! -name "*.cpp"\)| wc -l
Количество остальных файлов: 47122
```
6. Найдите полный пусть до файла any.hpp внутри библиотеки boost.
```
 $ find -name any.hpp
 Вывод: 
./boost_1_69_0/boost_1_69_0/boost/spirit/home/support/algorithm/any.hpp
./boost_1_69_0/boost_1_69_0/boost/any.hpp
./boost_1_69_0/boost_1_69_0/boost/proto/detail/any.hpp
./boost_1_69_0/boost_1_69_0/boost/fusion/include/any.hpp
./boost_1_69_0/boost_1_69_0/boost/fusion/algorithm/query/detail/any.hpp
./boost_1_69_0/boost_1_69_0/boost/fusion/algorithm/query/any.hpp
./boost_1_69_0/boost_1_69_0/boost/hana/fwd/any.hpp
./boost_1_69_0/boost_1_69_0/boost/hana/any.hpp
./boost_1_69_0/boost_1_69_0/boost/type_erasure/any.hpp
./boost_1_69_0/boost_1_69_0/boost/xpressive/detail/utility/any.hpp
```
7. Выведите в консоль все файлы, где упоминается последовательность boost::asio.
```
$ grep -r "boost::asio" //grep ищет последовательность boost::asio внутри всех файлов данного каталога параметр -r включает рекурсивный поиск и grep также ищет во всех подкаталогах
 Часть вывода:
 Rogopl/boost-libs/include/boost/beast/http/serializer.hpp:        boost::asio::const_buffer,               // chunk-ext
Rogopl/boost-libs/include/boost/beast/http/serializer.hpp:        boost::asio::const_buffer,               // chunk-ext
Rogopl/boost-libs/include/boost/beast/http/serializer.hpp:        boost::asio::const_buffer,               // chunk-size
Rogopl/boost-libs/include/boost/beast/http/serializer.hpp:        boost::asio::const_buffer,               // chunk-final
Rogopl/boost-libs/include/boost/beast/http/serializer.hpp:        boost::asio::const_buffer,               // trailers 
Rogopl/boost-libs/include/boost/beast/http/serializer.hpp:        boost::asio::const_buffer,               // chunk-ext
Rogopl/boost-libs/include/boost/beast/http/serializer.hpp:        boost::asio::const_buffer,               // chunk-final
Rogopl/boost-libs/include/boost/beast/http/serializer.hpp:        boost::asio::const_buffer,               // trailers
```
8. Скомпилирутйе boost. Можно воспользоваться инструкцией или ссылкой.
```
При попытке ввести ./bootstrap.sh --prefix=boost_output не было прав доступа. Решение этой проблемы такое:
$ sudo apt update - обновляем
$ sudo apt install build-essential - устанавилваем gcc пакет (вместе с библиотекой build-essential)
$ gcc --version - проверяем версию gcc
$ ./bootstrap.sh --prefix=boost_output --with-toolset=gcc - Вызываем необходимую нам команду с gcc
$ ./b2 install - Компилируем boost
```
9. Перенесите все скомпилированные на предыдущем шаге статические библиотеки в директорию ~/boost-libs.
```
Создаём папку ~/boost-libs: $ mkdir -p ./boost-libs
$ mv ~/boost_1_69_0/boost_output/include ~/Rogopl/boost-libs //mv перемещает папку/файл в другую директорию  
$ mv ~/boost_1_69_0/boost_output/lib ~/Rogopl/boost-libs
```
10. Подсчитайте сколько занимает дискового пространства каждый файл в этой директории.
```
$ du -a -h //du выводит размер всех файлов (параметр -a) в удобном для человека формате (параметр -h)
Часть вывода:
24K	./include/boost/format/parsing.hpp
8,0K	./include/boost/format/format_class.hpp
4,0K	./include/boost/format/free_funcs.hpp
4,0K	./include/boost/format/detail/workarounds_stlport.hpp
4,0K	./include/boost/format/detail/msvc_disambiguater.hpp
8,0K	./include/boost/format/detail/workarounds_gcc-2_95.hpp
4,0K	./include/boost/format/detail/config_macros.hpp
4,0K	./include/boost/format/detail/compat_workarounds.hpp
4,0K	./include/boost/format/detail/unset_macros.hpp
32K	./include/boost/format/detail
16K	./include/boost/format/feed_args.hpp
12K	./include/boost/format/format_implementation.hpp
20K	./include/boost/format/group.hpp
4,0K	./include/boost/format/exceptions.hpp
8,0K	./include/boost/format/alt_sstream.hpp
4,0K	./include/boost/format/format_fwd.hpp
16K	./include/boost/format/alt_sstream_impl.hpp
8,0K	./include/boost/format/internals.hpp
4,0K	./include/boost/format/internals_fwd.hpp
164K	./include/boost/format
155M	./include/boost
155M	./include
207M	.
```
11. Найдите топ10 самых "тяжёлых".
```
$ du -Sh | sort -rh | head -10 //-S не включает размер подпапок в размер папки, sort - сортирует файлы по размеру, head -10 вывести 10 первых таких файлов
Вывод:
52M	./lib
5,3M	./include/boost/fusion/container/generation/detail/preprocessed
5,1M	./include/boost/phoenix/statement/detail/preprocessed
4,5M	./include/boost/typeof
4,5M	./include/boost/phoenix/core/detail/cpp03/preprocessed
3,8M	./include/boost/geometry/srs/projections
2,7M	./include/boost/fusion/container/vector/detail/cpp03/preprocessed
2,0M	./include/boost/qvm/gen
2,0M	./include/boost/phoenix/scope/detail/cpp03/preprocessed
2,0M	./include/boost/numeric/ublas
```
