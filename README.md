# -3.-
Урок 3. Классы и объекты

1. Построить три класса (базовый и 2 потомка), описывающих некоторых работников с почасовой оплатой (один из потомков - Freelancer) и фиксированной оплатой (второй потомок -Worker).
а) Описать в базовом классе абстрактный метод для расчёта среднемесячной заработной платы.
Для «повременщиков» формула для расчета такова: «среднемесячная заработная плата = 20.8 * 8 * почасовая ставка», для работников с фиксированной оплатой «среднемесячная заработная плата = фиксированная месячная оплата».
б) Создать на базе абстрактного класса массив/коллекцию сотрудников и заполнить его.
в) ** Реализовать интерфейсы для возможности сортировки массива/коллекции (обратите ваше внимание на интерфейсы Comparator, Comparable), добавьте новое состояние на урове базового типа и создайте свой уникальный компаратор.
г) ** Создать класс, содержащий массив или коллекцию сотрудников (как Worker так и Freelancer), и реализовать возможность вывода данных с использованием foreach (подсказка: вам потребуется поработать с интерфейсом Iterable).


import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

// Базовый абстрактный класс Работник
abstract class Employee {
    private String name;

    public Employee(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }

    // Абстрактный метод для расчета среднемесячной заработной платы
    public abstract double calculateSalary();

    // Компаратор по имени работника
    public static Comparator<Employee> NameComparator = new Comparator<Employee>() {
        @Override
        public int compare(Employee e1, Employee e2) {
            return e1.getName().compareTo(e2.getName());
        }
    }
}

// Потомок класса Работник - Повременщик
class Freelancer extends Employee {
    private int hourlyRate;

    public Freelancer(String name, int hourlyRate) {
        super(name);
        this.hourlyRate = hourlyRate;
    }

    @Override
    public double calculateSalary() {
        return 20.8 * 8 * hourlyRate;
    }
}

// Потомок класса Работник - Работник с фиксированной оплатой
class Worker extends Employee {
    private double monthlySalary;

    public Worker(String name, double monthlySalary) {
        super(name);
        this.monthlySalary = monthlySalary;
    }

    @Override
    public double calculateSalary() {
        return monthlySalary;
    }
}

public class Main {
    public static void main(String[] args) {
        // Создаем список работников
        List<Employee> employees = new ArrayList<>();

        // Добавляем повременщика и работника с фиксированной оплатой в список
        employees.add(new Freelancer("Иван", 10));
        employees.add(new Worker("Петр", 5000));

        // Расчет среднемесячной заработной платы для каждого работника
        for (Employee employee : employees) {
            System.out.println(employee.getName() + ": " + employee.calculateSalary());
        }
        
        // Сортировка списка работников по имени с использованием компаратора
        Collections.sort(employees, Employee.NameComparator);

        // Вывод отсортированного списка работников
        System.out.println("Отсортированный список работников по имени:");
        for (Employee employee : employees) {
            System.out.println(employee.getName());
        }
    }
}
