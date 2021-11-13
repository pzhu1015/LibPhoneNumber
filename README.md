# LibPhoneNumber
vs2015 编译google C++的windows静态库，用于检测国际手机号, 

主要引用文件: PhoneNumber.h, PhoneNumberUtil.h, 但是使用时尽量使用智能指针，源始指针使用不小心容易内存泄露

```C++
#include <phonenumbers/phonenumber.h>
#include <phonenumbers/phonenumberutil.h>
using i18n::phonenumbers::PhoneNumberUtil;
using i18n::phonenumbers::PhoneNumber;
int main(char** argv, int argc)
{
	PhoneNumberUtil *phoneUtil = PhoneNumberUtil::GetInstance();
	//初始化一个电话号码
	PhoneNumber *pn = new PhoneNumber();
	pn->set_country_code(86);
	pn->set_national_number(13478808311);


	//判断电话号码是否有效
	std::cout << std::boolalpha << phoneUtil->IsValidNumber(*pn) << std::endl;

	//判断电话号码所在的地区
	std::string *region = new std::string();
	phoneUtil->GetRegionCodeForNumber(*pn, region);
	std::cout << *region << std::endl;


	std::string* name = new std::string();
	phoneUtil->GetNationalSignificantNumber(*pn, name);
	std::cout << *name << std::endl;


	//获取某个国家的国字区号
	PhoneNumber *example = new PhoneNumber();
	phoneUtil->GetInvalidExampleNumber("CN", example);
	std::cout << example->country_code() << std::endl;
	std::set<std::string> sets;
	phoneUtil->GetSupportedRegions(&sets);


	//释放内存
	delete pn;
	pn = nullptr;

	delete region;
	region = nullptr;

	delete name;
	name = nullptr;

	delete example;
	example = nullptr;

	system("pause");

	return 0;
}
```

