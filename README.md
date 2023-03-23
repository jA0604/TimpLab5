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

git submodule init && git submodule update

cmake -H. -B_build -DBUILD_TESTS=ON


![изображение](https://user-images.githubusercontent.com/112771063/227204923-b2d67148-08fa-467c-8674-7bb2a33da181.png)



cmake --build _build 



![изображение](https://user-images.githubusercontent.com/112771063/227209504-f02ab0ee-1b7f-462b-aae9-8cb1cf1f0189.png)


cmake --build _build --target test

_build/check







![изображение](https://user-images.githubusercontent.com/112771063/227214077-da91adca-cebf-422e-8dc2-e0feed38a151.png)






cmake --build _build --target test -- ARGS=--verbose





![изображение](https://user-images.githubusercontent.com/112771063/227224905-06983efb-8413-4a39-900a-1dd1d44c056a.png)




git add .

git commit -m 'added proj'

git push origin main 





![изображение](https://user-images.githubusercontent.com/112771063/227225142-4ed5e520-3cee-44c7-a096-7f1aa5a162cd.png)









![изображение](https://user-images.githubusercontent.com/112771063/227225245-4d54ed3c-6ca1-4383-a49b-0677ce6a1cb0.png)




