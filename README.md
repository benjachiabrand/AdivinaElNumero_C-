# AdivinaElNumero_C-
Programa simulando el juego "Adivina el numero random entre 1-100" utilizando bucles while y for, condicionales if, else if, arrays, vectores, funciones y procedimientos.

    internal class Program
    {
        static void Main(string[] args)
        {
            int[] intentosHistorial = new int[0];
            bool seJugoAlgunaPartida = false;
            intentosHistorial = JugarUnaPartida();
            seJugoAlgunaPartida = true;

           
            while (true)
            {
                MostrarMenu();
                int opcionMenu = PedirOpcionMenu();

                switch (opcionMenu)
                {
                    case 1:
                        intentosHistorial = JugarUnaPartida();
                        break;

                    case 2:
                        if (seJugoAlgunaPartida)
                            MostrarHistorial(intentosHistorial);
                        else
                            Console.WriteLine("No se ha jugado ninguna partida todavía.");
                        break;

                    case 3:
                        Console.WriteLine("¡Gracias por jugar! Hasta luego.");
                        return;

                    default:
                        Console.WriteLine("Opción inválida.");
                        break;
                }

                Console.WriteLine(); 
            }
        }

        static void MostrarMenu()
        {
            Console.WriteLine("========== MENÚ ==========");
            Console.WriteLine("1. Jugar otra vez");
            Console.WriteLine("2. Ver historial de la última partida");
            Console.WriteLine("3. Salir del programa");
        }

        static int PedirOpcionMenu()
        {
            Console.Write("Elija una opción: ");
            string entrada = Console.ReadLine();
            int.TryParse(entrada, out int opcion);
            return opcion;
        }

        static int GenerarNumeroSecreto()
        {
            Random rnd = new Random();
            return rnd.Next(1, 101); 
        }

        static bool ValidarEntrada(string input, out int numero)
        {
            bool esNumero = int.TryParse(input, out numero);
            return esNumero && numero >= 1 && numero <= 100;
        }

        static int[] JugarUnaPartida()
        {
            int maxIntentos = 7;
            int[] intentos = new int[maxIntentos];
            int intentosRealizados = 0;
            int numeroSecreto = GenerarNumeroSecreto();

            Console.WriteLine("\n¡Nueva Partida!");
            Console.WriteLine("Adiviná el número entre 1 y 100. Tenés 7 intentos.");

            while (intentosRealizados < maxIntentos)
            {
                Console.Write($"Intento #{intentosRealizados + 1}: ");
                string entrada = Console.ReadLine();

                if (!ValidarEntrada(entrada, out int intento))
                {
                    Console.WriteLine("Número inválido. Ingresá un número entre 1 y 100.");
                    continue;
                }

                intentos[intentosRealizados] = intento;
                intentosRealizados++;

                if (intento == numeroSecreto)
                {
                    Console.WriteLine($" ¡Felicitaciones! Adivinaste el número secreto ({numeroSecreto}) en {intentosRealizados} intentos.");
                    break;
                }
                else if (intento < numeroSecreto)
                {
                    Console.WriteLine("El número secreto es MAYOR.");
                }
                else
                {
                    Console.WriteLine("El número secreto es MENOR.");
                }
            }

            if (intentosRealizados == maxIntentos && intentos[intentosRealizados - 1] != numeroSecreto)
            {
                Console.WriteLine($"\n Se te acabaron los intentos. El número secreto era {numeroSecreto}.");
            }

            return RecortarArray(intentos, intentosRealizados);
        }

        static void MostrarHistorial(int[] intentos)
        {
            Console.WriteLine("\nHistorial de intentos de la última partida:");
            for (int i = 0; i < intentos.Length; i++)
            {
                Console.WriteLine($"Intento #{i + 1}: {intentos[i]}");
            }
        }

        static int[] RecortarArray(int[] original, int cantidad)
        {
            int[] nuevo = new int[cantidad];
            for (int i = 0; i < cantidad; i++)
            {
                nuevo[i] = original[i];
            }
            return nuevo;
        }
    }
}
