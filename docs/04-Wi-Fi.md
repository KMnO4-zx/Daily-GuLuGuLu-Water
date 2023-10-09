# ESP32 连接WiFi并发送请求

[在线模拟代码](https://wokwi.com/projects/378098916506519553)

ESP32内置WiFi模块，无需多余外部电路设计，真是太棒啦！

## 链接WiFi

下面是一些常用函数

1. `WiFi.begin(ssid, password)`：该函数用于连接到 Wi-Fi 网络。需要提供要连接的网络的 SSID 和密码作为参数。

2. `WiFi.disconnect()`：该函数用于断开当前的 Wi-Fi 连接。

3. `WiFi.status()`：该函数返回当前 Wi-Fi 连接的状态。返回值可能是以下之一： 

    - `WL_CONNECTED`：已连接到 Wi-Fi 网络。

    - `WL_DISCONNECTED`：未连接到 Wi-Fi 网络。

    - `WL_IDLE_STATUS`：Wi-Fi 处于空闲状态。

    - `WL_NO_SSID_AVAIL`：未找到指定的 Wi-Fi 网络。

4. `WiFi.localIP()`：该函数返回 ESP32 设备在 Wi-Fi 网络中分配的本地 IP 地址。

5. `WiFi.macAddress()`：该函数返回 ESP32 设备的 MAC 地址。

6. `WiFi.scanNetworks()`：该函数用于扫描周围可用的 Wi-Fi 网络。它返回一个整数，表示扫描到的网络数量。可以使用其他函数（如 `WiFi.SSID()` 和 `WiFi.RSSI()`）来获取每个网络的详细信息。

7. `WiFi.SSID(networkIndex)`：该函数返回指定索引的扫描到的 Wi-Fi 网络的 SSID。

8. `WiFi.RSSI(networkIndex)`：该函数返回指定索引的扫描到的 Wi-Fi 网络的信号强度（RSSI）

### 连接WiFi代码

```cpp
#include <WiFi.h>

// 定义板载LED引脚
#define LED 2

void setup() {
  // 设置波特率
  Serial.begin(9600);
  Serial.print("正在链接WiFi");
  // 填入wifi名称和密码
  WiFi.begin("Wokwi-GUEST", "", 6);
  // 如果没连上就一直连
  while (WiFi.status() != WL_CONNECTED) {
    delay(100);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println(" 连接成功!");
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  // 使用板载 LED 反馈连接成功
  pinMode(LED, OUTPUT);
  
  digitalWrite(LED, HIGH);
  delay(1000);
  digitalWrite(LED, LOW);
  delay(1000);

  digitalWrite(LED, HIGH);
  delay(1000);
  digitalWrite(LED, LOW);
  delay(1000);

  digitalWrite(LED, HIGH);
  delay(1000);
  digitalWrite(LED, LOW);
}
```

## 获取网络请求

以下是 `HTTPClient` 库的一些常用功能和函数：其实和python中的`requests`库没什么太大区别。

1. `HTTPClient http;`：创建 HTTPClient 对象。
2. `http.begin(url)`：指定要发送请求的 URL。
3. `http.addHeader(name, value)`：添加 HTTP 头部。
4. `http.setAuthorization(username, password)`：设置 HTTP 基本身份验证的用户名和密码。
5. `http.setTimeout(timeout)`：设置请求超时时间（以毫秒为单位）。
6. `http.GET()`：发送 GET 请求，并返回一个 HTTP 状态码。
7. `http.POST(payload)`：发送 POST 请求，并将 payload 作为请求正文。
8. `http.responseStatusCode()`：获取响应的状态码。
9. `http.responseHeaders()`：获取响应的头部。
10. `http.responseBody()`：获取响应的正文。
11. `http.getString()`：获取响应正文作为字符串。
12. `http.getStream()`：获取响应正文作为流对象。
13. `http.end()`：关闭连接并释放资源。

### 代码

访问一下百度

```cpp
#include <WiFi.h>
#include <HTTPClient.h>

#define LED 2

// 定义请求地址 直接就是一个访问百度
String url = "https://www.baidu.com/";

void setup() {
  Serial.begin(9600);
  Serial.print("正在链接WiFi");
  WiFi.begin("Wokwi-GUEST", "", 6);
  while (WiFi.status() != WL_CONNECTED) {
    delay(100);
    Serial.print(".");
  }
  Serial.println("");
  Serial.println(" 连接成功!");
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());

  // 创建 HTTPClient 对象
  HTTPClient http;

  // 发送GET请求
  http.begin(url);

  int httpCode = http.GET();

  // 获取响应状态码
  Serial.printf("HTTP 状态码: %d  ", httpCode);

  // 获取响应正文
  String response = http.getString();
  Serial.println("响应数据");
  Serial.println(response);

  http.end();

}

void loop() {
  // 使用板载 LED 反馈连接成功
  pinMode(LED, OUTPUT);
  
  digitalWrite(LED, HIGH);
  delay(1000);
  digitalWrite(LED, LOW);
  delay(1000);

  digitalWrite(LED, HIGH);
  delay(1000);
  digitalWrite(LED, LOW);
  delay(1000);

  digitalWrite(LED, HIGH);
  delay(1000);
  digitalWrite(LED, LOW);
}
```

