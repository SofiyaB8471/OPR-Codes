# OPR-Codes This repository contains all codes 8-11 laboratory works. By Sofiya Belodedova 713-2

#Laboratory work 8.1

public class Money
{
    private long rubles;
    private int kopeks;

    public Money(long rubles, int kopeks)
    {
        this.rubles = rubles;
        this.kopeks = kopeks;
    }

    public static Money operator +(Money m1, Money m2)
    {
        long totalRubles = m1.rubles + m2.rubles;
        int totalKopeks = m1.kopeks + m2.kopeks;

        if (totalKopeks >= 100)
        {
            totalRubles += totalKopeks / 100;
            totalKopeks = totalKopeks % 100;
        }

        return new Money(totalRubles, totalKopeks);
    }

    public static Money operator -(Money m1, Money m2)
    {
        long totalRubles = m1.rubles - m2.rubles;
        int totalKopeks = m1.kopeks - m2.kopeks;

        if (totalKopeks < 0)
        {
            totalRubles -= 1;
            totalKopeks += 100;
        }

        return new Money(totalRubles, totalKopeks);
    }

    public static Money operator /(Money m1, Money m2)
    {
        double totalAmount = (m1.rubles + (double)m1.kopeks / 100) / (m2.rubles + (double)m2.kopeks / 100);
        long totalRubles = (long)totalAmount;
        int totalKopeks = (int)((totalAmount - totalRubles) * 100);

        return new Money(totalRubles, totalKopeks);
    }

    public static Money operator /(Money m1, double number)
    {
        double totalAmount = (m1.rubles + (double)m1.kopeks / 100) / number;
        long totalRubles = (long)totalAmount;
        int totalKopeks = (int)((totalAmount - totalRubles) * 100);

        return new Money(totalRubles, totalKopeks);
    }

    public static Money operator *(Money m1, double number)
    {
        double totalAmount = (m1.rubles + (double)m1.kopeks / 100) * number;
        long totalRubles = (long)totalAmount;
        int totalKopeks = (int)((totalAmount - totalRubles) * 100);

        return new Money(totalRubles, totalKopeks);
    }

    public static bool operator >(Money m1, Money m2)
    {
        return (m1.rubles > m2.rubles) || (m1.rubles == m2.rubles && m1.kopeks > m2.kopeks);
    }

    public static bool operator <(Money m1, Money m2)
    {
        return (m1.rubles < m2.rubles) || (m1.rubles == m2.rubles && m1.kopeks < m2.kopeks);
    }

    public override string ToString()
    {
        return $"{rubles} рублей, {kopeks:00} копеек";
    }
}

public class Program
{
    public static void Main()
    {
        try
        {
            Console.Write("Введите количество рублей для денежки №1: ");
            long rubles;
            if (!long.TryParse(Console.ReadLine(), out rubles))
            {
                Console.WriteLine("Ошибка при вводе количества рублей. Вводите цифры, а не буквы");
                Console.Write("Введите количество рублей для денежки №1: ");
                Console.ReadLine();
            }
            else if (rubles < 0)
            {
                Console.WriteLine("Нельзя вводить отрицательное количество рублей");
                Console.Write("Введите количество рублей для денежки №1: ");
                Console.ReadLine();
            }
           
            Console.Write("Введите количество копеек для денежки №1: ");
            int kopeks;
            if (!int.TryParse(Console.ReadLine(), out kopeks))
            {
                Console.WriteLine("Ошибка при вводе количества копеек.Вводите цифры, а не буквы");
                Console.Write("Введите количество копеек для денежки №1: ");
                Console.ReadLine();
            }
            else if (kopeks < 0)
            {
                Console.WriteLine("Нельзя вводить отрицательное количество копеек");
                Console.Write("Введите количество копеек для денежки №1: ");
                Console.ReadLine();
            }

            Money amount1 = new Money(rubles, kopeks);

            Console.Write("\nВведите количество рублей для денежки №2: ");
            if (!long.TryParse(Console.ReadLine(), out rubles))
            {
                Console.WriteLine("Ошибка при вводе количества рублей. Вводите цифры, а не буквы");
            }
            else if (rubles < 0)
            {
                Console.WriteLine("Нельзя вводить отрицательное количество рублей");
                Console.Write("Введите количество рублей для денежки №2: ");
                Console.ReadLine();
            }
            

            Console.Write("Введите количество копеек для денежки №2: ");
            if (!int.TryParse(Console.ReadLine(), out kopeks))
            {
                Console.WriteLine("Ошибка при вводе количества копеек.Вводите цифры, а не буквы");
            }
            else if (kopeks < 0)
            {
                Console.WriteLine("Нельзя вводить отрицательное количество копеек");
                Console.Write("Введите количество копеек для денежки №2: ");
                Console.ReadLine();
            }
            


            Money amount2 = new Money(rubles, kopeks);

            Money sum = amount1 + amount2;
            Console.WriteLine("\nСумма денежек №1 и №2: " + sum);

            Money difference = amount1 - amount2;
            Console.WriteLine("\nРазность денежек №1 и №2: " + difference);

            // Деление получившихся чисел друг на друга, т.е 1/2
            Money division = amount1 / amount2;
            Console.WriteLine("\nДеление №1 на №2: " + division);

            // Деление №1 на дробное число
            Console.Write("\nВведите дробное число для деления денежки №1: ");
            double number;
            if (!double.TryParse(Console.ReadLine(), out number))
            {
                Console.WriteLine("Ошибка при вводе числа. Необходимо ввести цифры, а не буквы");
                Console.Write("\nВведите дробное число для деления денежки №1: ");
                Console.ReadLine();
            }
            else if (number< 0)
            {
                Console.WriteLine("Нельзя вводить отрицательное значение делителя");
                Console.Write("\nВведите дробное число для деления денежки №1: ");
                Console.ReadLine();
            }

            Money divisionByNumber = amount1 / number;
            Console.WriteLine("Результат деления денежки №1: " + divisionByNumber);



            // Деление суммы №2 на дробное число
            Console.Write("\nВведите дробное число для деления денежки №2: ");
            double number1;
            if (!double.TryParse(Console.ReadLine(), out number1))
            {
                Console.WriteLine("Ошибка при вводе числа. Необходимо ввести цифры, а не буквы");
                Console.Write("\nВведите дробное число для деления денежки №2: ");
                Console.ReadLine();
            }
            else if (number1 < 0)
            {
                Console.WriteLine("Нельзя вводить отрицательное значение делителя");
                Console.Write("\nВведите дробное число для деления денежки №2: ");
                Console.ReadLine();
            }

            Money divisionByNumber1 = amount2 / number1;
            Console.WriteLine("Результат деления денежки №2: " + divisionByNumber1);



            // Умножение №1 на дробное число
            Console.Write("\nВведите дробное число для умножения денежки №1: ");
            if (!double.TryParse(Console.ReadLine(), out number))
            {
                Console.WriteLine("Ошибка при вводе числа. Необходимо ввести цифры, а не буквы");
                Console.Write("\nВведите дробное число для умножения денежки №1: ");
                Console.ReadLine();
            }
            else if (number < 0)
            {

                Console.WriteLine("Нельзя вводить отрицательное значение для множителя");
                Console.Write("\nВведите дробное число для умножения денежки №1: ");
                Console.ReadLine();
            }

            Money multiplication = amount1 * number;
            Console.WriteLine("Результат умножения денежки №1 на число: " + multiplication);

            // Умножение №2 на дробное число
            Console.Write("\nВведите дробное число для умножения денежки №2: ");
            if (!double.TryParse(Console.ReadLine(), out number1))
            {
                Console.WriteLine("Ошибка при вводе числа.Необходимо ввести цифры, а не буквы");
                Console.Write("\nВведите дробное число для умножения денежки №2: ");
                Console.ReadLine();
            }
            else if (number1 < 0)
            {

                Console.WriteLine("Нельзя вводить отрицательное значение для множителя");
                Console.Write("\nВведите дробное число для умножения денежки №2: ");
                Console.ReadLine();
            }


            Money multiplication1 = amount2 * number1;
            Console.WriteLine("Результат умножения денежки №2 на число: " + multiplication1);
            // Итоги
            Console.WriteLine("Сравнение сумм: ");
            if (amount1 > amount2)
            {
                Console.WriteLine("№1 больше, чем №2");
            }
            else
            {
                Console.WriteLine("№2 больше, чем №1");
            }
        }
        catch (FormatException) { Console.WriteLine("Было введено некорректное значение"); }

    }
}






#Laboratory work 8.2
using System;

class Goods
{
    public string name;
    public DateTime date;
    public double price;
    public int countGoods;
    public string idNumber;


    public void ChangePrice(double newPrice)
    {
        if (newPrice > 0)
        {
            //price = newPrice;
            Console.WriteLine("Цена товара успешно изменена");
        }
       // else
        //{
            //Console.WriteLine("Некорректное значение цены");
        //}
    }

    public void ChangeQuantity(int change)
    {
        countGoods += change;
        Console.WriteLine("Количество товара успешно изменено");
    }

    public double CalculateCost()
    {
        return price * countGoods;
    }

    public string ShowCost()
    {
        return $"Стоимость товара: {CalculateCost()}";
    }
}

public class Program
{
    public static void Main()
    {


        Goods goods = new Goods();

        Console.WriteLine("Наименование товара: ");
        goods.name = Console.ReadLine();

        try
        {
            Console.WriteLine("Введите дату в формате ДД.ММ.ГГГГ");
            int date;
            DateTime dat = Convert.ToDateTime(Console.ReadLine());
            if (!int.TryParse(Console.ReadLine(), out date))
            {
                Console.WriteLine("Ошибка при вводе даты");
            }
            goods.date = Convert.ToDateTime(Console.ReadLine());
        }
        catch (FormatException)
        {
            Console.WriteLine("Неверный формат ввода даты!");
            Console.WriteLine("\nВведите дату в формате ДД.ММ.ГГГГ");
            Console.ReadLine();      
        }

        Console.Write("\nЦена товара: ");
        double priceInput = Convert.ToDouble(Console.ReadLine());
        if (priceInput < 0)
        {
            Console.WriteLine("Цена товара не может быть отрицательной!!!!");
            Console.Write("Цена товара: ");
            double priceInput1 = Convert.ToDouble(Console.ReadLine());
        }
        else
        {
            goods.price = priceInput;
        }

        Console.Write("\nКоличество единиц товара: ");
        int countInput = Convert.ToInt32(Console.ReadLine());
        if (countInput < 0)
        {
            Console.WriteLine("Количество единиц товара не может быть отрицательным!!!");
            Console.Write("Количество единиц товара: ");
            int countInput1 = Convert.ToInt32(Console.ReadLine());
        }
        else
        {
            goods.countGoods = countInput;
        }

        Console.Write("\nНомер накладной: ");
        double idNumberInput = Convert.ToDouble(Console.ReadLine());
        if (idNumberInput < 0)
        {
            Console.WriteLine("Номер накладной не может быть отрицательным!");
            Console.Write("Номер накладной: ");
            double idNumberInput2 = Convert.ToDouble(Console.ReadLine());
        }
        else
        {
            goods.idNumber = Convert.ToString(Console.ReadLine());
        }

        Console.WriteLine("\nС этим товаром все, спасибо!\nДля изменения стоимости и количества товара нажмите enter");
        Console.ReadKey();

        Console.WriteLine("\nВведите новую цену товара:");
        double newPrice = double.Parse(Console.ReadLine());
        if (newPrice < 0)
        {
            Console.WriteLine("Новая цена товара не может быть отрицательной");
            Console.WriteLine("\nВведите новую цену товара:");
            Console.ReadLine();
        }
        goods.ChangePrice(newPrice);

        Console.WriteLine("\nВведите изменение количества товара:");
        int change = int.Parse(Console.ReadLine());
        if (change < 0)
        {
            Console.WriteLine("Новое количество товаров не может быть отрицательным");
            Console.WriteLine("\nВведите изменение количества товара:");
            Console.ReadLine();
        }
        goods.ChangeQuantity(change);


        Console.WriteLine(goods.ShowCost());

    }

}






#Laboratory work 9
using System;
using System.Collections.Generic;
public class ChessPiece
{
    public int x; //горизонталь
    public int y; //вертикаль

    public ChessPiece(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

    //  метод, который возвращает список фигур, которые может убить текущая фигура
    public virtual List<string> GetPossibleCaptures()
    {
        return new List<string>();
    }
}

public class Ferz : ChessPiece
{
    public Ferz(int x, int y) : base(x, y)
    {

        
    }

    public override List<string> GetPossibleCaptures()
    {
        List<string> possibleCaptures = new List<string>();

        // Проверяем горизонталь и вертикаль
        for (int i = 0; i < 8; i++)
        {
            if (i != x) // Не учитываем текущую позицию ферзя
            {
                possibleCaptures.Add($"{i},{y}");
                possibleCaptures.Add($"{x},{i}");
            }
        }
        // Проверяем диагонали
        for (int i = 1; x + i < 8 && y + i < 8; i++)
        {
            possibleCaptures.Add($"{x + i},{y + i}");
        }
        for (int i = 1; x - i >= 0 && y - i >= 0; i++)
        {
            possibleCaptures.Add($"{x - i},{y - i}");
        }
        for (int i = 1; x + i < 8 && y - i >= 0; i++)
        {
            possibleCaptures.Add($"{x + i},{y - i}");
        }
        for (int i = 1; x - i >= 0 && y + i < 8; i++)
        {
            possibleCaptures.Add($"{x - i},{y + i}");
        }
        Console.WriteLine("Фигуры, которые может убить выбранная фигура:\n");
        Console.WriteLine("Ферзь может убить пешку");
        Console.WriteLine("Ферзь может убить ладью");
        Console.WriteLine("Ферзь может убить слона");
        Console.WriteLine("Ферзь может убить коня");

        return possibleCaptures;
    }
}

public class Peshka : ChessPiece
{
    public Peshka(int x, int y) : base(x, y)
    {

    }

    public override List<string> GetPossibleCaptures()
    {
        List<string> possibleCaptures = new List<string>();
        for (int i = 0; i < 8; i++)
        {
            if (i != x) // Не учитываем текущую позицию ферзя
            {
                possibleCaptures.Add($"{i},{y}");
                possibleCaptures.Add($"{x},{i}");
            }
        }
        // Проверяем диагонали
        for (int i = 1; x + i < 8 && y + i < 8; i++)
        {
            possibleCaptures.Add($"{x + i},{y + i}");
        }
        for (int i = 1; x - i >= 0 && y - i >= 0; i++)
        {
            possibleCaptures.Add($"{x - i},{y - i}");
        }
        for (int i = 1; x + i < 8 && y - i >= 0; i++)
        {
            possibleCaptures.Add($"{x + i},{y - i}");
        }
        for (int i = 1; x - i >= 0 && y + i < 8; i++)
        {
            possibleCaptures.Add($"{x - i},{y + i}");
        }
        Console.WriteLine("Фигуры, которые может убить выбранная фигура:\n");
        Console.WriteLine("Пешка может убить ладью");
        Console.WriteLine("Пешка может убить слона");
        Console.WriteLine("Пешка может убить коня");
        Console.WriteLine("Пешка может срубить вышеперечисленные фигуры только если они окажутся наискосок от нее!");

        return possibleCaptures;
    }
}

public class Horse : ChessPiece
{
    public Horse(int x, int y) : base(x, y)
    {

    }

    public override List<string> GetPossibleCaptures()
    {
        List<string> possibleCaptures = new List<string>();

        for (int i = 1; x + i < 8 && y + i < 8; i++)
        {
            possibleCaptures.Add($"{x + i},{y + i}");
        }
        for (int i = 1; x - i >= 0 && y - i >= 0; i++)
        {
            possibleCaptures.Add($"{x - i},{y - i}");
        }
        for (int i = 1; x + i < 8 && y - i >= 0; i++)
        {
            possibleCaptures.Add($"{x + i},{y - i}");
        }
        for (int i = 1; x - i >= 0 && y + i < 8; i++)
        {
            possibleCaptures.Add($"{x - i},{y + i}");
        }
        Console.WriteLine("Фигуры, которые может убить выбранная фигура:\n");
        Console.WriteLine("Конь может срубить любую фигуру, если та окажется на конечной точке его хода ");

        return possibleCaptures;
    }
}

// Главный класс программы
public class Program
{
    public static void Main(string[] args)
    {
        // Ввод позиции фигуры и создание объекта выбранного класса
        try
        {
            Console.WriteLine("Введите позицию фигуры (например, 'A1'): ");
            string position = Console.ReadLine();
            if (position == null)
            {
                Console.WriteLine("Позиция фигуры не может быть равно нулю!");
            }

            int x = position[0] - 'A' + 1; // конвертируем букву в число
            int y;
            if (!int.TryParse(position[1].ToString(), out y))
            {
                Console.WriteLine("Некорректный ввод координаты Y.");
                return;
            }

            ChessPiece selectedPiece;

            Console.WriteLine("Выберите фигуру (1 - ферзь, 2 - пешка, 3 - конь): ");
            int choice;
            if (!int.TryParse(Console.ReadLine(), out choice))
            {
                Console.WriteLine("Некорректный выбор фигуры.");
                Console.WriteLine("Выберите фигуру (1 - ферзь, 2 - пешка, 3 - конь): ");
                Console.ReadLine();
            }
            

            switch (choice)
            {
                case 1:
                    selectedPiece = new Ferz(x, y);
                    break;
                case 2:
                    selectedPiece = new Peshka(x, y);
                    break;
                case 3:
                    selectedPiece = new Horse(x, y);
                    break;
                default:
                    Console.WriteLine("Некорректный выбор фигуры.");
                    return;
            }

            // Выводим список фигур, которые может убить выбранная фигура
            List<string> possibleCaptures = selectedPiece.GetPossibleCaptures();

        }
        catch (System.IndexOutOfRangeException) { Console.WriteLine("Программа требует значение буква + цифра, а не только цифра/буква"); }
        catch (FormatException) { Console.WriteLine("Программа требует значение буква + цифра, а не только цифра/буква"); }
    }
}




#Laborartory work 10.1
using System;
using System.Windows.Forms;

namespace Laba10
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            double res;
            double p = 1030;
            double v;

            try
            {
                v = Convert.ToDouble(textBox1.Text); //ввожу литры
                if (v > 0)
                {
                    res = (v * 0.001) * p;

                    label2.Text = res.ToString("n") + " масса молока в кг";
                }
                else
                {
                    label2.Text = ("Вы не можете вводить \nотрицательное значение!");
                }


            }
            catch (FormatException) { label2.Text = ("Буквы вводить нельзя"); };

        }

        private void textBox3_TextChanged(object sender, EventArgs e)
        {

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }

        private void ВходныеДанные_Layout(object sender, LayoutEventArgs e)
        {

        }
    }

}





#Laboratory work 10.2
using System;
using System.Windows.Forms;


namespace Laba10._2
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            double x;
            double y;
            double z;

            try
            {
                x = Convert.ToDouble(textBox1.Text);
                y = Convert.ToDouble(textBox2.Text);
                z = Convert.ToDouble(textBox3.Text);
                double minNum = Math.Min(Math.Min(x, y), z);
                double maxNum = Math.Max(Math.Max(x, y), z);

                label7.Text = maxNum.ToString();
                label8.Text = minNum.ToString();

            }
            catch (FormatException)
            {
                label9.Text = ("Буквы вводить нельзя, программа только для чисел!");
            }
           

        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {

        }

        private void label4_Click(object sender, EventArgs e)
        {

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }

        private void button1_Click(object sender, MouseEventArgs e)
        {

        }

        private void label7_Click(object sender, EventArgs e)
        {

        }

        private void label9_Click(object sender, EventArgs e)
        {
            
        }

        private void button2_Click(object sender, EventArgs e)
        {
            textBox1.Clear();
            textBox2.Clear();
            textBox3.Clear();
            label7.Text = string.Empty;
            label8.Text = string.Empty;
            label9.Text = string.Empty;
        }
    }
}





#Laboratory work 11.1
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Laba11._1
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void label1_Click(object sender, EventArgs e) //это то окно, где цифры в зависимости от прокрутки меняются
        {

        }

        private void trackBar1_Scroll(object sender, EventArgs e) //лента прокрутки
        {
            label1.Text = trackBar1.Value.ToString();
            int n = trackBar1.Value;
            int sum = 0;
            for (int i = 1; i <= n; i++)
            {
                sum += 2 * i;
            }
            label4.Text = sum.ToString(); //счетчик, когда считается с использованием цикла

            int fSum = n * (n + 1);
            label7.Text = fSum.ToString(); //счетчик, когда считается по формуле
        }

        private void label3_Click(object sender, EventArgs e) //заголовок
        {

        }
    }
}





#Laboratory work 11.2
using System;
using System.Collections.Generic;
using System.Data;
using System.IO;
using System.Linq;
using System.Linq.Expressions;
using System.Windows.Forms;

namespace ОПРР_4._2
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            using (StreamWriter writer = new StreamWriter("flights.txt"))
            {
                foreach (var aeroflot in notes)
                {
                    writer.WriteLine($"{aeroflot.type},{aeroflot.number},{aeroflot.pynktnaznachenuya}");
                }
            }
            foreach (var note in notes)
            {
                listBox1.Items.Add(note);
            }
        }

        class Aeroflot
        {
            public string type { get; set; }
            public string number { get; set; }
            public string pynktnaznachenuya { get; set; }


            public override string ToString()
            {
                return $"{type}; {number}; {pynktnaznachenuya}";
            }
        }

        List<Aeroflot> notes = new List<Aeroflot>();
        private void button2_Click(object sender, EventArgs e) //генерация
        {
            int[] lala = new int[10];
            Random random = new Random();

            List<string> type = new List<string> { "Airbus А320", "Airbus А321", "Airbus А330", "Boeing 737", "Boeing 777", "Sukhoi Superjet 100" };
            List<string> pynktnaznachenuya = new List<string> { "Москва - Казань", "Москва - Санкт-Петербург", "Баку - Москва", "Казань - Москва", "Москва - Абакан", "Омск - Нижний Новгород", "Новосибирск - Москва", "Санкт - Петербург - Тольятти", "Сочи - Казань" };
            List<string> number = new List<string> { "SU1498", "SU1496", "SU1462", "SU1444", "SU1851", "SU1855", "SU1857", "SU1986", "SU1235", "SU1474" };


            for (int i=0; i != 10; i++)
            {
                Aeroflot note = new Aeroflot();
                {
                    note.type = type[random.Next(type.Count)];
                    note.pynktnaznachenuya = pynktnaznachenuya[random.Next(pynktnaznachenuya.Count)];
                    note.number = number[random.Next(number.Count)];
                };
                notes.Add(note);
            }

            notes = notes.OrderBy(x => x.number).ToList();
            foreach (var note in notes)
            {
                listBox1.Items.Add($"{note.type} - {note.number} - {note.pynktnaznachenuya}");
            }
        }

        private void button1_Click_1(object sender, EventArgs e) //очистка = удаление строчки
        {
            if (listBox1.SelectedIndex != -1) // Проверка, что выбрана запись для удаления (выделяется цветом)
            {
                listBox1.Items.RemoveAt(listBox1.SelectedIndex); // Удаление выделенной записи из списка
            }
        }

        private void button3_Click(object sender, EventArgs e)//сортировка
        {

        }

        private void textBox1_TextChanged(object sender, EventArgs e)
        {
            
        }

        private void button4_Click(object sender, EventArgs e)//фильтрация
        {
            string pynktnaznacheniya1 = textBox1.Text;
            var results = notes.Where(x => x.pynktnaznachenuya == pynktnaznacheniya1).ToList(); // Фильтрация записей по пункту назначения

            if (results.Any())
            {
                // Очистка списка и добавление отфильтрованных записей
                foreach (var result in results)
                {
                    listBox2.Items.Add($"{result.type} - {result.number} - {result.pynktnaznachenuya}");
                }
            }
            else
            {
                listBox2.Items.Clear();
                textBox1.Text =  textBox1.Text + "  " + "Не найдено"; // Вывод сообщения, если записи не найдены
            }
        }
        private void listBox1_Click(object sender, EventArgs e)
        {

        }


    }
}
