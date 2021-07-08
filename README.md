# MAIN (C#)


using MathFinal.DataSet1TableAdapters;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace MathFinal
{
    class Program
    {
        static void Main(string[] args)
        {
            //VARIABLES
            MatrizTableAdapter adapter = new MatrizTableAdapter();
            int x = 0;
            int y = 0;
            int[,] X = new int[3, 3];
            byte choice;

            //MAIN
            Console.WriteLine("Digite sus 9 valores");
            while (true) 
            {
                Console.WriteLine("\ndigite un valor");
                X[y, x] = Convert.ToInt32(JustNumbers());
                if (y == 2 && x == 2) 
                {
                    break;
                }
                if (x == 2) 
                {
                    x = 0;
                    x--;
                    y++;
                    Console.WriteLine("\n");
                }
                x++;
            }
            Console.WriteLine("Que desea hacer?");
            Console.WriteLine("1: Sumar");
            Console.WriteLine("2: Restar");
            choice = Convert.ToByte(JustNumbers());
            switch (choice)
            {
                case 1:
                    adapter.Sumarr(X[0, 0], X[0, 1], X[0, 2], X[1, 0], X[1, 1], X[1, 2], X[2, 0], X[2, 1], X[2, 2]);
                    Console.Clear();
                    Console.WriteLine("Suma realizada");
                    Console.WriteLine("información insertada:");
                    x = 0; y = 0;
                    while (true)
                    {
                        Console.Write(X[y,x] + "\t");

                        if (y == 2 && x == 2)
                        {
                            break;
                        }
                        if (x == 2)
                        {
                            x = 0;
                            x--;
                            y++;
                            Console.WriteLine("\n");
                        }
                        x++;
                    }
                    Console.ReadKey();
                    break;
                case 2:
                    adapter.restar(X[0, 0], X[0, 1], X[0, 2], X[1, 0], X[1, 1], X[1, 2], X[2, 0], X[2, 1], X[2, 2]);
                    Console.Clear();
                    Console.WriteLine("Resta realizada");
                    Console.WriteLine("información insertada:");
                    x = 0; y = 0;
                    while (true)
                    {
                        
                        Console.Write(X[y, x] + "\t");

                        if (y == 2 && x == 2)
                        {
                            break;
                        }
                        if (x == 2)
                        {
                            x = 0;
                            x--;
                            y++;
                            Console.WriteLine("\n");
                        }
                        x++;
                    }
                    Console.ReadKey();
                    break;
            }
        }
        //Funciones
        static string JustNumbers()
        {
            ConsoleKey k;
            string data = "";
            do
            {
                var inf = Console.ReadKey(true);
                k = inf.Key;
                int val;
                bool ex = int.TryParse(inf.KeyChar.ToString(), out val);

                if (k == ConsoleKey.Backspace && data.Length > 0)
                {
                    Console.Write("\b \b");
                    data = data.Remove(data.Length - 1);
                }
                else if (!Char.IsControl(inf.KeyChar) && ex)
                {
                    Console.Write(inf.KeyChar);
                    data += inf.KeyChar;
                }
            } while (k != ConsoleKey.Enter);
            System.Console.WriteLine("\n");
            return data;
        }
    }
}

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# TABLA DE LA BASE DE DATOS.

CREATE TABLE [dbo].[Matriz] (
    [Id]     INT IDENTITY (1, 1) NOT NULL,
    [X]      INT NULL,
    [Y]      INT NULL,
    [Result] INT NULL,
    PRIMARY KEY CLUSTERED ([Id] ASC)
);

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

# PROCEDEURS UTILIZADOS

# SUMAR

CREATE PROCEDURE [dbo].[Sumarr]
	@X00 int,
	@X01 int,
	@X02 int,
	@X10 int,
	@X11 int,
	@X12 int,
	@X20 int,
	@X21 int,
	@X22 int
AS

		update Matriz set
		X = X + @X00,
		Y = Y + @X01,
		Result = Result + @X02
		where Id = 1

		update Matriz set
		X = X + @X10,
		Y = Y + @X11,
		Result = Result + @X12
		where Id = 2

		update Matriz set
		X = X + @X20,
		Y = Y + @X21,
		Result = Result + @X22
		where Id = 3

RETURN 0

# RESTAR

CREATE PROCEDURE [dbo].[restar]
	@X00 int,
	@X01 int,
	@X02 int,
	@X10 int,
	@X11 int,
	@X12 int,
	@X20 int,
	@X21 int,
	@X22 int
AS

		update Matriz set
		X = X - @X00,
		Y = Y - @X01,
		Result = Result - @X02
		where Id = 1

		update Matriz set
		X = X - @X10,
		Y = Y - @X11,
		Result = Result - @X12
		where Id = 2

		update Matriz set
		X = X - @X20,
		Y = Y - @X21,
		Result = Result - @X22
		where Id = 3

RETURN 0
