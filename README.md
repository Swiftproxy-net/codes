using System.Net;
using System.Threading;

var handler = new HttpClientHandler
{
    UseProxy = true
};
var proxy = new WebProxy("http://us.swiftproxy.net:7878");
var proxyUsername = "username_custom_zone_us";
var proxyPass = "password";
proxy.Credentials = new NetworkCredential(proxyUsername, proxyPass);
handler.Proxy = proxy;
var httpClient = new HttpClient(handler);

httpClient.Timeout = TimeSpan.FromSeconds(15);

var task = httpClient.GetStringAsync("http://ipinfo.io/json");
task.Wait();
Console.WriteLine(task.Result);
