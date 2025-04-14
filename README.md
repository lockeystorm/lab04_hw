## Homework for Lab03

<details>
  <summary>Задание 1</summary>
  <p>
    
Вам поручили перейти на систему автоматизированной сборки **CMake**.
Исходные файлы находятся в директории [formatter_lib](formatter_lib).
В этой директории находятся файлы для статической библиотеки *formatter*.
Создайте `CMakeList.txt` в директории [formatter_lib](formatter_lib),
с помощью которого можно будет собирать статическую библиотеку *formatter*.

Клонируем репозиторий tp-labs/lab03 в локальный lab03_hw

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

Удаляем связь локального репозитория с исходным и связываем с пустым удаленным репозиторием lab03_hw, после делаем `--force push`

```
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

Создаем CMake-файл

```
$ touch CMakeList.txt
$ vim CMakeLists.txt
$ cat CMakeLists.txt
  cmake_minimum_required(VERSION 3.30)
  project(formatter)
  
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  
  set(LIB_SOURCE formatter.h formatter.cpp)
  
  add_library(formatter STATIC ${LIB_SOURCE})
  
  target_include_directories(formatter PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
```

Выполняем сборку

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
  -- Build files have been written to: /home/storm/lockeystorm/workspace/tasks/lab03_hw/formatter_lib/build

$ cmake --build build
  [ 50%] Building CXX object CMakeFiles/formatter.dir/formatter.cpp.o
  [100%] Linking CXX static library libformatter.a
  [100%] Built target formatter
```
  </p>
</details> 

<details>
  <summary>Задание 2</summary>
  <p>

У компании "Formatter Inc." есть перспективная библиотека,
которая является расширением предыдущей библиотеки. Т.к. вы уже овладели
навыком созданием `CMakeList.txt` для статической библиотеки *formatter*, ваш 
руководитель поручает заняться созданием `CMakeList.txt` для библиотеки 
*formatter_ex*, которая в свою очередь использует библиотеку *formatter*.

Создаем CMake-файл для formatter_ex

```
$ cd formatter_ex_lib
$ touch CMakeLists.txt
$ vim CMakeLists.txt
$ cat CMakeLists.txt
  cmake_minimum_required(VERSION 3.30)
  project(formatter_ex)
  
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  
  add_subdirectory(../formatter_lib formatter)
  
  add_library(formatter_ex STATIC formatter_ex.cpp formatter_ex.h)
  
  target_include_directories(formatter_ex PUBLIC ../formatter_lib ${CMAKE_CURRENT_SOURCE_DIR})
  
  target_link_libraries(formatter_ex PUBLIC formatter)
```

Запускаем сборку

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
  -- Configuring done (0.9s)
  -- Generating done (0.0s)
  -- Build files have been written to: /home/storm/lockeystorm/workspace/tasks/lab03_hw/formatter_ex_lib/build

$ cmake --build build
  [ 25%] Building CXX object formatter/CMakeFiles/formatter.dir/formatter.cpp.o
  [ 50%] Linking CXX static library libformatter.a
  [ 50%] Built target formatter
  [ 75%] Building CXX object CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
  [100%] Linking CXX static library libformatter_ex.a
  [100%] Built target formatter_ex
```
  </p>
</details>

<details>
  <summary>Задание 3</summary>
  <p>
    
Конечно же ваша компания предоставляет примеры использования своих библиотек.
Чтобы продемонстрировать как работать с библиотекой *formatter_ex*,
вам необходимо создать два `CMakeList.txt` для двух простых приложений:
* *hello_world*, которое использует библиотеку *formatter_ex*;
* *solver*, приложение которое испольует статические библиотеки *formatter_ex* и *solver_lib*.

Создаем CMake-файл для hello_world

```
$ cd hello_world_application
$ touch CMakeLists.txt
$ vim CMakeLists.txt
$ cat CMakeLists.txt
  cmake_minimum_required(VERSION 3.30)
  project(hello_world)
  
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  
  add_subdirectory(../formatter_ex_lib formatter_ex)
  
  add_executable(hello_world hello_world.cpp)
  
  target_link_libraries(hello_world formatter_ex)
```

И производим сборку

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
  -- Configuring done (0.5s)
  -- Generating done (0.0s)
-- Build files have been written to: /home/storm/lockeystorm/workspace/tasks/lab03_hw/hello_world_application/build

$ cmake --build build
  [ 16%] Building CXX object formatter_ex/formatter/CMakeFiles/formatter.dir/formatter.cpp.o
  [ 33%] Linking CXX static library libformatter.a
  [ 33%] Built target formatter
  [ 50%] Building CXX object formatter_ex/CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
  [ 66%] Linking CXX static library libformatter_ex.a
  [ 66%] Built target formatter_ex
  [ 83%] Building CXX object CMakeFiles/hello_world.dir/hello_world.cpp.o
  [100%] Linking CXX executable hello_world
  [100%] Built target hello_world
```

Создаем CMake-файл для библиотеки solver_lib

```
$ cd ../solver_lib
$ touch CMakeLists.txt && vim CMakeLists.txt
$ cat CMakeLists.txt
  cmake_minimum_required(VERSION 3.30)
  project(solver)
  
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  
  add_library(solver STATIC solver.h solver.cpp)
  
  target_include_directories(solver PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
```

Сборка:

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
  -- Configuring done (0.5s)
  -- Generating done (0.0s)
  -- Build files have been written to: /home/storm/lockeystorm/workspace/tasks/lab03_hw/solver_lib/build

$ cmake --build build
  [ 50%] Building CXX object CMakeFiles/solver.dir/solver.cpp.o
  [100%] Linking CXX static library libsolver.a
  [100%] Built target solver
```

Создаем CMake-файл для solver_application(equation)

```
$ cd ../solver_application
$ touch CMakeLists.txt && vim CMakeLists.txt
$ cat CMakeLists.txt
  cmake_minimum_required(VERSION 3.30)
  project(equation)
  
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  
  add_subdirectory(../formatter_ex_lib formatter_ex)
  add_subdirectory(../solver_lib solver)
  
  add_executable(equation equation.cpp)
  
  target_link_libraries(equation formatter_ex solver)
```

Собираем

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
  -- Configuring done (0.0s)
  -- Generating done (0.0s)
-- Build files have been written to: /home/storm/lockeystorm/workspace/tasks/lab03_hw/solver_application/build

$ cmake --build build
  [ 12%] Building CXX object solver/CMakeFiles/solver.dir/solver.cpp.o
  [ 25%] Linking CXX static library libsolver.a
  [ 25%] Built target solver
  [ 37%] Building CXX object formatter_ex/formatter/CMakeFiles/formatter.dir/formatter.cpp.o
  [ 50%] Linking CXX static library libformatter.a
  [ 50%] Built target formatter
  [ 62%] Building CXX object formatter_ex/CMakeFiles/formatter_ex.dir/formatter_ex.cpp.o
  [ 75%] Linking CXX static library libformatter_ex.a
  [ 75%] Built target formatter_ex
  [ 87%] Building CXX object CMakeFiles/equation.dir/equation.cpp.o
  [100%] Linking CXX executable equation
  [100%] Built target equation
```
  </p>
</details>
