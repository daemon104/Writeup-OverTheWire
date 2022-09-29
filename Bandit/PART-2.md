Over The Wire Bandit Part 2
===

16 levels sau của Over The Wire bandit

Link: https://overthewire.org/wargames/bandit/bandit0.html

---
## Mục lục <a name="menu"></a>

* [Mục lục](#menu)
* [Level 18](#t18)
* [Level 19](#t19)
* [Level 20](#t20)
* [Level 21](#t21)
* [Level 22](#t22)
* [Level 23](#t23)
* [Level 24](#t24)
* [Level 25](#t25)
* [Level 26](#t26)
* [Level 27](#t27)
* [Level 28](#t28)
* [Level 29](#t29)
* [Level 30](#t30)
* [Level 31](#t31)
* [Level 32](#t32)
* [Level 33](#t33)

---
## Level 18 <a name="t18"></a>

Ở level này, như đề gợi ý thì chúng ta không thể login bình thường cào server được vì đã khi log in vào sẽ lập tức bị log out ra, do đó, chúng ta sẽ sử dụng pseudo-terminal và tự tạo 1 shell sh cho mình bằng cách thêm /bin/sh sau câu lệnh ssh:

![](https://i.imgur.com/HCFet8y.png)

Sau khi vào được thì chúng ta chỉ việc cat file readme để lấy key

*Key obtained: awhqfNnAbc1naukrpqDYcF95h7HoMTrC*

---
## Level 19 <a name="t19"></a>

Ở level này, chúng ta sẽ dùng setuid binary trong home dir, đó là file bandit20-do, dùng thử thì thấy được cú pháp của nó, file này cho phép thực thi câu lệnh dưới quyền của user bandit20, do đó ta sẽ tiến hành cat file password của level 20 bằng bandit20-do:

![](https://i.imgur.com/R0yUCvy.png)

*Key obtained: VxCazJaVykI6W36BkBU0mJTCM8rR95XT*

---
## Level 20 <a name="t20"></a>

Đối với level này, chúng ta cần tạo 2 terminal để đáp ứng yêu cầu đề, 1 terminal để lắng nghe port 4444 và đưa lên nội dung password level 20, 1 terminal dùng để chạy file suconnect và nhận nội dung ở port 4444:

* Terminal 1:
![](https://i.imgur.com/znxrZ3e.png)

* Terminal 2:
![](https://i.imgur.com/PgmCjBl.png)

Sau khi terminal 2 read xong password và thấy khớp thì password level kế tiếp sẽ hiện ra ở terminal 1

![](https://i.imgur.com/oLzhEpR.png)

*Key obtained: NvEJF7oVjkddltPSrdKEFOllh9V1IBcq*

---
## Level 21 <a name="t21"></a>

Ở level này, chúng ta cần xem cron đang thực thi tự động câu lệnh nào bằng cách cd tới đường dẫn /etc/cron.d, sau đó, chúng ta cat file cronjob_bandit22 và thu được kết quả như sau:

![](https://i.imgur.com/Tck0yLT.png)

Ta thấy user bandit22 đang thực thi file bandit22.sh chuyển kết quả về /dev/null, do đó, chúng ta cần đọc file bandit22.sh:

![](https://i.imgur.com/WpohEYQ.png)

Kết quả thu được là bash script này thực hiện đọc password của bandit level 22 và send nó vào /tmp/...., vì thế, chúng ta chỉ cần cat file đó là thu được password

*Key obtained: WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff* 

---
## Level 22 <a name="t22"></a>

Ở level này, chúng ta thực hiện tương tự level trước nhưng khác hơn xíu là phải đọc file sh xem nó làm gì:

![](https://i.imgur.com/Apjpdpk.png)

Cơ bản là file script này sẽ dùng gán câu echo kìa sau khi hash bằng md5 và tách khoảng trắng ra cho biến $target, sau đó copy nội dung file password tới /tmp/$target. Do đó, chúng ta chỉ cần test thử câu echo là có được kết quả:

![](https://i.imgur.com/6PbOWqG.png)

Ra được đoạn hash, chỉ cần đọc file /tmp/$target là được:

![](https://i.imgur.com/pYBF3si.png)

*Key obtained: QYw0Y2aiA672PsMmh9puTQuhoz8SyR2G*

---
## Level 23 <a name="t23"></a>

Đối với level này, khi thực hiện tương tự 2 level trước thì ta thấy file sh lần này phức tạp hơn:

![](https://i.imgur.com/KpU2Zrg.png)

Đoạn script này có tác dụng là duyệt folder /var/spool/bandit24/foo và thực thi mọi script tìm thấy với user bandit24, sau đó xóa bỏ các script. Do đó, chúng ta cần viết script đọc file pass của level 24 tại /tmp/... sau đó copy vô /var/spool/bandit24/foo và chờ nó thực thi:

File script.sh:
![](https://i.imgur.com/jQ3MS38.png)

Copy và chờ kết quả:
![](https://i.imgur.com/BZHX8LQ.png)

*Key obtained: VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar*

---
## Level 24 <a name="t24"></a>

Ở level này, đề yêu cầu chúng ta tương tác với daemon đang lắng nghe ở port 30002, đưa vào password của level này và 4 kí tự mã pin, 4 kí tự này chỉ có thể bruteforce ra (trong khoảng 0-9999). Do đó, chúng ta sẽ viết script bruteforce:

![](https://i.imgur.com/Z9xxcel.png)

Script này sẽ lặp for, gán i bằng lần lượt từng giá trị trong output câu lệnh seq tạo ra 1 dãy số từ 0-9999 ghép vào password level 24 và đưa nó vào nc

Sau đó chỉ cần chmod, chạy nó và xem kết quả:

![](https://i.imgur.com/DzkDH5e.png)

*Key obtained: p7TaowMYrmu23Ol8hiZh9UvD0O9hpx8d*

---
## Level 25 <a name="t25"></a>

Ở level này, sau khi đăng nhập vào thì chúng ta nhận được 1 ssh private key cho level 26 nhưng theo đề nói thì ssh bằng key này sẽ không trả về shell /bin/bash mà là 1 shell khác, do đó, chúng ta tiến hành kiểm tra như sau:

![](https://i.imgur.com/0y1qSSc.png)

Có thể thấy là bandit26 đang sử dụng showtext shell:

![](https://i.imgur.com/faSesKr.png)

Sau khi cat, chúng ta thấy được đoạn script trên, khi ta kết nối ssh tới bandit26 nó sẽ chạy lệnh more in đoạn text trong file text.txt, xong rồi exit ngay lập tức. Do đó, chúng ta phải sử dụng trick để tăng thời gian lệnh more in ra đoạn text bằng cách thu nhỏ kích thước terminal lại ở mức nhỏ nhất, trong khoảng thời gian more đang in text, chúng ta sẽ bấm "v" để chạy vào editor của more (đọc man more), từ đây chúng ta có thể lấy được shell /bin/sh:

![](https://i.imgur.com/MU6MDwX.png)

![](https://i.imgur.com/qHCHezk.png)

Sau đó, ta gõ câu lệnh sau để lấy shell /bin/sh:

![](https://i.imgur.com/o5QAXDH.png)

Thành công có được shell sh, tiến hành lấy lại password cho level này:

![](https://i.imgur.com/wOkzrjO.png)

*Key obtained: c7GvcKlw9mC7aUQaPx7nwFstuAIBw1o1*

---
## Level 26 <a name="t26"></a>

Đối với level này, khi nhận được shell ở level trên, chúng ta tiến hành ls và thấy file bandit27-do giống ở 1 level chúng ta đã giải lúc trước, chỉ cần nhập câu lệnh cat password bandit27:

![](https://i.imgur.com/QZnFV1y.png)

*Key obtained: YnQpBuifNMas1hcUFk70ZmqkhUU2EuaS*

---
## Level 27 <a name="t27"></a>

Ở level này, chúng ta cần tạo 1 folder tên bất kì trong thư mục /tmp để clone repo về với cú pháp như sau:

![Uploading file..._re8dkv0ns]()

Sau đó cat file README trong repo là được:

![](https://i.imgur.com/1OL5wqz.png)

*Key obtained: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s*

---
## Level 28 <a name="t28"></a>

Level này cũng giống level trước, phải tải repo về để tìm kiếm password, nhưng lần này trong file README không có password:

![](https://i.imgur.com/uJvIBeb.png)

Do đó, chúng ta cần đọc commit log và xem sự thay đổi, sau đó đọc file readme trước khi bị thay đổi để lấy password level sau:

![](https://i.imgur.com/IUMCvEE.png)

![](https://i.imgur.com/cMcmzcp.png)

![](https://i.imgur.com/1YGJNWS.png)

*Key obtained: tQKvmcwNYcFS6vmPHIUSI3ShmsrQZK8S*

---
## Level 29 <a name="t29"></a>

Ở level này, chúng ta thực hiện clone repo tương tự như 2 level trước, sau đó bắt đầu tìm kiếm password, đầu tiên ta check git log nhưng không thấy gì khả quan:

![](https://i.imgur.com/rt0Wp9S.png)

Tiếp theo, ta check các branch, có thể dùng params "-r" để xem các branch bị ẩn mặc định dành cho dev:

![](https://i.imgur.com/AlTuzox.png)

Thử với branch dev, chúng ta xem log của nó và thấy 1 commit có thể chứa pass:

![](https://i.imgur.com/QiI5Vxr.png)

Thử với 2 commit đầu tiên thì tìm được password:

![](https://i.imgur.com/wSCV7dw.png)

*Key obtained: xbhV3HpNGlTIdnjUrdAlPzc2L6y9EOnS*

---
## Level 30 <a name="t30"></a>

Ở level này, độ khó được nâng lên chút, sau khi thực hiện tương tự 2 level trên, xem log và branch nhưng không thu được gì quan trọng, do đó, chúng ta cần tìm trong file .git xem có gì không:

![](https://i.imgur.com/UOSqAfU.png)

Sau khi tìm kiếm xung quanh thì thấy được 1 file chứa thông tin khả quan, đó là file packed-refs:

![](https://i.imgur.com/aazH8Nw.png)

Cat file thì thu được 2 đoạn hash của 2 refs, dùng lệnh show để xem refs secret thì tìm được password:

![](https://i.imgur.com/J01PAeh.png)

*Key obtained: OoffzGDlzhAlerFJ2cAiz1D41JW1Mhmt*

---
## Level 31 <a name="t31"></a>

Ở level này, chúng ta thực hiện clone về và cat file README.md, trong file yêu cầu ta push 1 file key.txt với content chỉ định lên master để lấy password cho level sau, chúng ta chỉ việc tạo và push file lên là được:

![](https://i.imgur.com/RO5zVaS.png)

![](https://i.imgur.com/Q8m163l.png)

![](https://i.imgur.com/XA1TXoB.png)

*Key obtained: rmCBvG56y58BXzv98yZGdO7ATVL5dW8y*

---
## Level 32 <a name="t32"></a>

Ở level này, sau khi connect vào thì chúng ta được cấp 1 cái shell đặc biệt, gọi là uppercase shell, shell này sẽ uppercase mọi command mình nhập vào khiến cho chúng ta không làm được gì cả:

![](https://i.imgur.com/IfxkwOB.png)

Nhưng nó có 1 quy tắc, thông thường khi nhận input từ user, terminal sẽ quy định nhận tham số theo format $n (với n là số thứ tự của params), ví dụ:

```
nmap -v -T4 < ipv4 >
```
 
Trong ví dụ trên, $0=shell, $1=-v, $2=-T4, $3=ip

Khi chúng ta nhập bất cứ lệnh gì thì nó sẽ được uppcase lên và đưa cho $0 (là shell sh) để thực thi, do đó, chúng ta chỉ cần gọi shell sh mà không dùng bất kì command nào khác, khi đó sẽ gọi được shell thật sự:

![](https://i.imgur.com/5uCcX64.png)

![](https://i.imgur.com/z9niGET.png)

*Key obtained: odHo63fHiFqcWWJG9rLiLDtPm45KzUKy*

---
## Level 33 <a name="t33"></a>

Đây là level cuối của challege bandit:

![](https://i.imgur.com/ks08MN1.png)

---
