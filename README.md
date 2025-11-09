using System;
using System.Net.Sockets;
using System.Threading.Tasks;

namespace NetScanner
{
    class Program
    {
        static async Task Main(string[] args)
        {
            Console.Write("Enter IP address: ");
            string host = Console.ReadLine();
            Console.Write("Enter port range (e.g. 20-100): ");
            string[] range = Console.ReadLine().Split('-');

            int start = int.Parse(range[0]);
            int end = int.Parse(range[1]);

            for (int port = start; port <= end; port++)
            {
                await CheckPort(host, port);
            }
        }

        static async Task CheckPort(string host, int port)
        {
            using (TcpClient client = new TcpClient())
            {
                try
                {
                    await client.ConnectAsync(host, port);
                    Console.WriteLine($"[+] Port {port} open");
                }
                catch
                {
                    // Closed port
                }
            }
        }
    }
}
