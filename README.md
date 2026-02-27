
## 1. Mục đích

Bài thực hành này giúp sinh viên: 
- Nhận biết lỗ hổng Signature Malleability trong thuật toán ECDSA
- Hiểu ảnh hưởng của nó trong giao dịch blockchain (Ethereum, Bitcoin)
- Biết cách phát hiện và phòng tránh tấn công này

------------------------------------------------------------------------

## 2. Yêu cầu đối với sinh viên

-   Nắm kiến thức cơ bản về ECDSA, chữ ký số, txid và hashing\
-   Có kỹ năng đọc/ghi tệp JSON\
-   Sử dụng terminal và thao tác cơ bản trong môi trường Labtainers

------------------------------------------------------------------------

## 3. Nội dung thực hành

### Chuẩn bị lab

``` bash
imodule https://github.com/NKTriS/labtainer/raw/main/imodule.tar
labtainer malleability
```

> Lưu ý: Sinh viên nhập tên tài khoản (MSV) khi được yêu cầu trong
> terminal để lưu kết quả chấm điểm.

------------------------------------------------------------------------

## Nhiệm vụ 1: Tạo chữ ký gốc (signer)

``` bash
sudo chmod 777 /shared
python3 signer.py
```

Kết quả: - /shared/original_signature.json - /shared/public_key.txt -
/shared/original_txid.txt

------------------------------------------------------------------------

## Nhiệm vụ 2: Tạo chữ ký giả (attacker)

``` bash
python3 attacker.py
```

-   Nếu đã chuẩn hóa low-s → dừng và báo lỗi\
-   Nếu chưa → tạo malleable_signature.json và malleable_txid.txt

------------------------------------------------------------------------

## Nhiệm vụ 3: Kiểm tra tính hợp lệ (victim)

``` bash
python3 verify.py
cat /shared/verify_result.txt
```

------------------------------------------------------------------------

## Nhiệm vụ 4: Vô hiệu hóa chuẩn hóa chữ ký

Comment đoạn:

``` python
# if s > SECP256k1.order // 2:
#     print("Rejected: Signature has high-s value → vulnerable to malleability")
#     return False
```

Chạy lại signer → attacker → verify.

------------------------------------------------------------------------

## Nhiệm vụ 5: So sánh chữ ký

``` bash
python3 plot_sig_diff.py
```

Quan sát: - r giống nhau\
- s đảo dấu\
- txid khác nhau

------------------------------------------------------------------------

## Nhiệm vụ 6: Blockchain

``` bash
python3 blockchain.py --safe
```

Log: - blockchain_log.txt - replay_log.txt

------------------------------------------------------------------------

## Kết thúc lab

``` bash
stoplab
labtainer -r malleability
checkwork <tên bài lab>
```
