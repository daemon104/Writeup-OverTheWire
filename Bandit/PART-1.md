Over The Wire - Bandit Part 1
===

18 levels đầu của Over The Wire bandit

Link: https://overthewire.org/wargames/bandit/bandit0.html

---
## Mục lục <a name="menu"></a>

* [Mục lục](#menu)
* [Level 0](#t0)
* [Level 1](#t1)
* [Level 2](#t2)
* [Level 3](#t3)
* [Level 4](#t4)
* [Level 5](#t5)
* [Level 6](#t6)
* [Level 7](#t7)
* [Level 8](#t8)
* [Level 9](#t9)
* [Level 10](#t10)
* [Level 11](#t11)
* [Level 12](#t12)
* [Level 13](#t13)
* [Level 14](#t14)
* [Level 15](#t15)
* [Level 16](#t16)
* [Level 17](#t17)

---
## Level 0 <a name="t0"></a>

Chúng ta cần ssh tới server của OTW:

![](https://i.imgur.com/P95pdKi.png)

Chúng ta sẽ dùng 'ls' để list nội dung của directory, sau đó dùng lệnh cat file readme để lấy key tiến tới level sau:

![](https://i.imgur.com/EI2z3Kp.png)

Cứ mỗi lần có key level, chúng ta sẽ cần ssh tới server với username tùy theo level để tiếp tục các thử thách

![](https://i.imgur.com/do5wDrU.png)

*Key obtained: NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL*

---
## Level 1 <a name="t1"></a>

Ơ level này, ta cần cat file "-", để làm vậy, chúng ta sẽ thêm "<" vào phía trước tên file:

![](https://i.imgur.com/r0pTl2L.png)

*Key obtained: rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi*

---
## Level 2 <a name="t2"></a>

Ở level này, chúng ta sẽ cat file có khoảng trắng, chúng ta sẽ thêm cặp nháy đơn vào để thực hiện hoặc dùng dấu '\':

![](https://i.imgur.com/3fmXvpU.png)

*Key obtained: aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG*

---
## Level 3 <a name="t3"></a>

Ở level này, chúng ta gặp phải file ẩn trong dir, do đó, ta cần thực hiện ls với flag -a để list toàn bộ file, gồm cả file ẩn, sau đó cat nó với cú pháp sau:

![](https://i.imgur.com/wRQXcFO.png)

*Key obtained: 2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe* 

---
## Level 4 <a name="t4"></a>

Ở level này, có rất nhiều file trong thư mục inhere nhưng hầu hết trong số chúng đều không đọc được, chỉ duy nhất 1 cái có nội dung rõ ràng, vì vậy, chúng ta phải cat thử toàn bộ:

![](https://i.imgur.com/ESWBLnX.png)

*Key obtained: lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR*

---
## Level 5 <a name="t5"></a>

Với level này, vì có rất nhiều dir nên việc tìm từng cái rất mất thời gian, để đáp ứng 3 yêu cầu, ta sử dụng tổ hợp câu lệnh sau:

```
find . -type f -size 1033c ! -executable -exec file {} + | grep -w text
```

* "find . -type f": để tìm file trong thư mục hiện tại
* "-size 1033c": size là 1033 bytes
* "! -executable": lấy kết quả ngược lại với executable là non-executable
* "-exec file {} + | grep -w text": thực thi câu lệnh file với output, grep các file có nội dung loại text

![](https://i.imgur.com/W6QmsUg.png)


*Key obtained: P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU

---
## Level 6 <a name="t6"></a>

Đối với level này, chúng ta sẽ sử dụng câu lệnh find để tìm file thỏa mãn 3 yêu cầu đề cho, cú pháp câu lệnh như sau:

![](https://i.imgur.com/M67a2Uq.png)

* "-type f": để tìm file, không directory hay thứ gì khác
* "-user -group": chỉ định user và group sở hữu file này
* "2>/dev/null": những dòng in ra lỗi do tìm không thấy hoặc permission denied thì cho vô /dev/null

*Key obtained: z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S*

---
## Level 7 <a name="t7"></a>

Ở level này, chúng ta cần cat file data.txt và grep output với từ khóa "millionth" để lọc được key:

![](https://i.imgur.com/iOwPEYG.png)

*Key obtained: TESKZC0XvTetK0S9xNwm25STk5iWrBvP*

---
## Level 8 <a name="t8"></a>

Đối với level này, chúng ta sẽ kết hợp lệnh sort với lệnh uniq:

![](https://i.imgur.com/weEpxTP.png)

Trước hết chúng ta sẽ sort output theo bảng chữ cái rồi sau đó dùng uniq với flag "-u" để lọc ra dòng duy nhất. Lí do cần dùng sort là vì nếu chỉ cat và uniq thì lệnh uniq nó sẽ không xét dòng duy nhất nếu các dòng đó không liền kề nhau, nên ta phải sort nó theo bảng chữ cái trước rồi uniq thì được

*Key obtained: EN632PlfYiZbn3PhVK3XOGSlNInNE00t*

---
## Level 9 <a name="t9"></a>

Ở level này, chúng ta sẽ sử dụng lệnh strings để in ra những dòng string mà chúng ta đọc được, sau đó pipeline cho grep, chúng ta sẽ grep 3 kí tự "=" vì trong đề nói là several kí tự

![](https://i.imgur.com/HtEY8Ye.png)

*Key obtained: G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s*

---
## Level 10 <a name="t10"></a>

Ở level này, chúng ta cần decode đoạn ciphertext trong file data.txt:

![](https://i.imgur.com/y8Eh4WR.png)

*Key obtained: 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM*

---
## Level 11 <a name="t11"></a>

Đối với level này, chúng ta sẽ dùng câu lệnh tr để thay thế các chữ cái trong file data.txt:

![](https://i.imgur.com/ivOQ7If.png)

Với câu lệnh trên, các chữ cái lần lượt thay đổi thành chữ cái khác, ví dụ: A chuyển sang N, B sang O,... M sang Z,... bảng chữ cái thường cũng vậy

*Key obtained: JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv*

---
## Level 12 <a name="t12"></a>

Ở level này, trước hết, chúng ta cần làm theo hướng dẫn của đề là tạo thư mục mới trong tmp và cp file vào:

![](https://i.imgur.com/PNR4Vv7.png)

Tiếp đó, ta tiến hành revert file data hexdump:

![](https://i.imgur.com/IRubRvp.png)

Lúc này file vẫn chưa đọc được vì nó đã bị nén nhiều lần, do đó, ta dùng lệnh file để xem coi nó bị nén bằng công vụ gì để có thể giải nén bằng công cụ đó:

![](https://i.imgur.com/F9wPmWv.png)

![](https://i.imgur.com/Twc9hKv.png)

Câu lệnh mv được sử dụng để đổi extension của file cho đúng với công cụ sử dụng (ví dụ: gzip nén và giải nén file .gz nên cần đổi tên thành .gz, 1 số trường hợp không cần làm vậy)

*Key obtained: wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw*

---
## Level 13 <a name="t13"></a>

Đối với level này, chúng ta được cấp 1 ssh private key để login vào user bandit14 và đi tiếp, do đó, trước hết chúng ta sẽ cat file ssh key và sao chép nó qua máy local của chúng ta, đặt tên là key.txt:

![](https://i.imgur.com/3e7r9PL.png)

![](https://i.imgur.com/Rk2o5Cw.png)

![](https://i.imgur.com/OCpX5EZ.png)

Tiếp theo, chúng ta sẽ dùng ssh với option "-i" dùng private key để kết nối tới server:

![](https://i.imgur.com/NbOzhJf.png)

![](https://i.imgur.com/KHgsnLx.png)

Kết nối tới server xong, chúng ta tiến hành cat file /etc/bandit_pass/bandit14 để lấy key level 14 (dùng sẽ tiện hơn file ssh key)

*Key obtained: fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq*

---
## Level 14 <a name="t14"></a>

Ở level này, đề yêu cầu kết nối tới localhost port 30000 bằng password vừa lấy được (pass cho level 14), do đó chúng ta sẽ cat file password rồi lấy output chuyển cho nc để kết nối tới localhost và lấy password cho level tiếp theo:

![](https://i.imgur.com/mTHun3Z.png)

*Key obtained: jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt*

---
## Level 15 <a name="t15"></a>

Level này cũng gần giống level trước nhưng cần sử dụng công nghệ SSL/TLS. Cụ thể chúng ta sẽ tiến hành thiết lập 1 kết nối bảo mật giữa máy tính với server trên localhost. Để thực hiện kết nối, ta sử dụng câu lệnh sau:

![](https://i.imgur.com/hNcWwZB.png)

Câu lệnh này sẽ kết nối client với server localhost đồng thời hiển thị chi tiết quá trình kết nối, flow của nó như sau:
* step 1: client gửi yêu cầu kết nối và mật khẩu chứng thực tới server
* step 2: server phản hồi bằng cert ssl của nó
* step 3: client verify cái cert, nếu ok thì thông báo cho server là chấp nhận
* step 4: server gửi chữ kí số dùng để mã hóa giải mã thông tin liên lạc 2 bên
* step 5: kết nối được thiết lập

Do mình bị lỗi READ_R_BLOCK nên mình thử dùng -ign_eof gián tiếp bằng cách dùng -quiet để output gọn lại:

![](https://i.imgur.com/cOfgvWC.png)

*Key obtained: JQttfApK4SeyHwDlI9SXGR50qclOAil1*

---
## Level 16 <a name="t16"></a>

Đối với level này, để thỏa mãn yêu cầu đề, ta sử dụng nmap với tổ hợp option như sau:

```
nmap -vv -T4 -Pn -p31000-32000 -sV localhost
```

* -vv: hiển thị chi tiết
* -T4: tốc độ scan
* -Pn: không ping, mặc định là server đang up
* -p31000-32000: chỉ scan các port trong khoảng
* -sV: scan service đang chạy trên từng port

Kết quả trả về cho thấy các port đang listening và service của chúng:

![](https://i.imgur.com/8uyjK8s.png)

Ta thấy port 31790 đang chạy service ssl, thử kết nối đến nó xem sao:

![](https://i.imgur.com/b2xNgke.png)

Thành công lấy được private key để log vào level sau.

Tiến hành ssh và cat file /etc/bandit_pass/bandit17 để lấy pass level 17 thuận tiện hơn cho việc login:

![](https://i.imgur.com/wvkizy8.png)

*Key obtained: VwOSWtCA7lRKkTfbr2IDh6awj9RNZM5e*

---
## Level 17 <a name="t17"></a>

Ở level này, để tìm ra dòng bị thay đổi ở file password.new ta dùng câu lệnh grep như sau:

![](https://i.imgur.com/eiVDA4S.png)

* -f: lấy file 1 (password.old) làm chuẩn để lọc
* -F: xem file 1 như là fixed string, là đoạn string đã bị thay đổi
* -w: tìm dòng giống nhau giữa 2 file
* -v: in ra dòng không giống giữa 2 file (loại output của -w)

*Key obtained: hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg*

---
