cmake_minimum_required(VERSION 3.4)

project (banking)
  
  #set(CMAKE_CXX_STANDARD 11)
  
  set(CMAKE_CXX_STANDARD 17)
  set(CMAKE_CXX_STANDARD_REQUIRED ON)
  
  #Добавляем опцию BUILD_TESTS. Если она включена, вместе с самой библиотекой собираются тесты 
  option(BUILD_TESTS "Build tests" OFF)
  
  if(BUILD_TESTS)                   # Если надо собрать тесты, добавляем опцию компилятора —coverage,
    add_compile_options(--coverage) # которая оставляет после прогонки кода отчёт о покрытии
  endif()
  
  
  
  #Делаем библиотеку account и добавляем директорию с заголовками
  add_library(account STATIC ${CMAKE_CURRENT_SOURCE_DIR}/banking/Account.cpp)
  target_include_directories(account PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/banking)
  
  #Делаем библиотеку transaction и добавляем директорию с заголовками
  add_library(transaction STATIC ${CMAKE_CURRENT_SOURCE_DIR}/banking/Transaction.cpp)
  target_include_directories(transaction PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/banking)
  
  #add_library(banking STATIC ${CMAKE_CURRENT_SOURCE_DIR}/banking/Transaction.cpp ${CMAKE_CURRENT_SOURCE_DIR}/banking/Account.cpp)
  #target_include_directories(banking PUBLIC
  #${CMAKE_CURRENT_SOURCE_DIR}/banking )
  
  #Линкуем к библиотеке gcov - он нужен для отчётов о покрытии
  target_link_libraries(banking gcov)
  
  #Собираем тесты из исходников, лежащих в директории tests
  if(BUILD_TESTS)
    enable_testing()
    add_subdirectory(third-party/gtest)
    file(GLOB BANKING_TEST_SOURCES tests/*.cpp)
    add_executable(check ${BANKING_TEST_SOURCES})
    target_link_libraries(check banking gtest_main)
    add_test(NAME check COMMAND check)
  endif()
