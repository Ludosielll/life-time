#include <iostream>
#include <ctime>
using namespace std;
int main() {
	int day, year, mounth;

	// Просим ввести дату рождения
	setlocale(LC_ALL, "Russian");
	cout << "Введите дату рождения (год месяц день)" << endl;
	cin >> year >> mounth >> day;

	// Просим ввести сегодняшнюю дату
	int daynow, yearnow, mounthnow;
	cout << "Введите сегодняшнюю дату (год месяц день)" << endl;
	cin >> yearnow >> mounthnow >> daynow;

	// создание обьектов даты рождения
	std::tm birthDate = {};
	birthDate.tm_year = year - 1900; // отсчёт с 1900 года
	birthDate.tm_mon = mounth - 1; // отсчёт с января (от нуля)
	birthDate.tm_mday = day;

	// создание обьектов сегодняшней даты
	std::tm currentDate = {};
	currentDate.tm_year = yearnow - 1900;
	currentDate.tm_mon = mounthnow - 1; // отсчёт с января (от нуля)
	currentDate.tm_mday = daynow;

	// Перевод из tm в time_t
	std::time_t birthDatees = std::mktime(&birthDate);
	std::time_t currentDatee = std::mktime(&currentDate);

	// проверяем на корректность преобразование времени
	if (birthDatees == -1 || currentDatee == -1) {
		cerr << "Ошибка преобразования времени." << endl;
		return 1;
	}

	// Вычисление преобразование в дни
	auto duration = std::difftime(currentDatee, birthDatees);
	auto days = duration / (60 * 60 * 24); // Преобразование секунд в дни

	// Вывод результата
	cout << "Вы прожили " << static_cast<long>(days) << " дней." << endl;

	return 0;
}
