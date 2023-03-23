cd Green-Ace/workspace

git clone git@github.com:Green-Ace/TimpLab5.git

mkdir third-party

git submodule add https://github.com/google/googletest third-party/gtest

git add third-party/gtest

mkdir tests

cat >> tests/test1.cpp <<EOF

#include <Account.h>
#include <gtest/gtest.h>
// Тест на проверку правильности конструктора
TEST(Account, Constructor)
{
Account a(2,300);

EXPECT_EQ(a.id(),2);
EXPECT_EQ(a.GetBalance(),300);
}
// Тест на проверку правильность изменения баланса
TEST(Account, ChangeBalance)
{
  Account a(2,300);
  a.Lock();
  a.ChangeBalance(100);
  EXPECT_EQ(a.GetBalance(),400);
}
// Тест на проверку состояния аккаунта(открыт/закрыт)
TEST(Account, Lock)
{
  Account a(2,300);
  a.Lock();
  a.ChangeBalance(100);
  a.Unlock();
  EXPECT_EQ(a.GetBalance(),400);
}
EOF

cmake -H. -B_build -DBUILD_TESTS=ON


![изображение](https://user-images.githubusercontent.com/112771063/227204923-b2d67148-08fa-467c-8674-7bb2a33da181.png)



cmake --build _build 



![изображение](https://user-images.githubusercontent.com/112771063/227209504-f02ab0ee-1b7f-462b-aae9-8cb1cf1f0189.png)


cmake --build _build --target test

_build/check







![изображение](https://user-images.githubusercontent.com/112771063/227214077-da91adca-cebf-422e-8dc2-e0feed38a151.png)









git add .

git commit -m 'added proj'

git push origin main 
