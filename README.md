## Homework

### Задание 1
Вам поручили перейти на систему автоматизированной сборки **CMake**.
Исходные файлы находятся в директории [formatter_lib](formatter_lib).
В этой директории находятся файлы для статической библиотеки *formatter*.
Создайте `CMakeList.txt` в директории [formatter_lib](formatter_lib),
с помощью которого можно будет собирать статическую библиотеку *formatter*.

```
$ git clone https://github.com/tp-labs/lab03 lab03_hw
  Cloning into 'lab03_hw'...
  remote: Enumerating objects: 91, done.
  remote: Counting objects: 100% (30/30), done.
  remote: Compressing objects: 100% (9/9), done.
  remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61 (from 1)
  Receiving objects: 100% (91/91), 1.02 MiB | 3.18 MiB/s, done.
  Resolving deltas: 100% (41/41), done.
```

```
$ git remote remove origin
$ git remote remove origin
$ git remote add origin https://github.com/lockeystorm/lab03_hw.git
$ git push --force origin master
  Enumerating objects: 91, done.
  Counting objects: 100% (91/91), done.
  Compressing objects: 100% (47/47), done.
  Writing objects: 100% (91/91), 1.02 MiB | 104.83 MiB/s, done.
  Total 91 (delta 41), reused 91 (delta 41), pack-reused 0 (from 0)
  remote: Resolving deltas: 100% (41/41), done.
  To https://github.com/lockeystorm/lab03_hw.git
   + f99ca16...94afc96 master -> master (forced update)
```
 
```
$ touch CMakeList.txt
$ vim CMakeLists.txt
$ cat CMakeLists.txt
  cmake\_minimum_required(VERSION 3.30)
  project(formatter)
  
  set(CMAKE\_CXX_STANDARD 11)
  set(CMAKE\_CXX_STANDARD_REQUIRED ON)
  
  set(LIB_SOURCE formatter.h formatter.cpp)
  
  add\_library(formatter STATIC ${LIB_SOURCE})
  
  target\_include\_directories(formatter PUBLIC "${CMAKE\_CURRENT\_SOURCE_DIR}")
```

```
$ cmake -B build
  -- The C compiler identification is GNU 14.2.0
  -- The CXX compiler identification is GNU 14.2.0
  -- Detecting C compiler ABI info
  -- Detecting C compiler ABI info - done
  -- Check for working C compiler: /usr/bin/cc - skipped
  -- Detecting C compile features
  -- Detecting C compile features - done
  -- Detecting CXX compiler ABI info
  -- Detecting CXX compiler ABI info - done
  -- Check for working CXX compiler: /usr/bin/c++ - skipped
  -- Detecting CXX compile features
  -- Detecting CXX compile features - done
  -- Configuring done (0.7s)
  -- Generating done (0.0s)
  -- Build files have been written to: /home/storm/lockeystorm/workspace/tasks/lab03\_hw/formatter_lib/build
```

```
$ cmake --build build
  [ 50%] Building CXX object CMakeFiles/formatter.dir/formatter.cpp.o
  [100%] Linking CXX static library libformatter.a
  [100%] Built target formatter
```

### Задание 2
У компании "Formatter Inc." есть перспективная библиотека,
которая является расширением предыдущей библиотеки. Т.к. вы уже овладели
навыком созданием `CMakeList.txt` для статической библиотеки *formatter*, ваш 
руководитель поручает заняться созданием `CMakeList.txt` для библиотеки 
*formatter_ex*, которая в свою очередь использует библиотеку *formatter*.

### Задание 3
Конечно же ваша компания предоставляет примеры использования своих библиотек.
Чтобы продемонстрировать как работать с библиотекой *formatter_ex*,
вам необходимо создать два `CMakeList.txt` для двух простых приложений:
* *hello_world*, которое использует библиотеку *formatter_ex*;
* *solver*, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.

