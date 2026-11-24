# Kapro AI · KapraoTiny-1.6M

KapraoTiny-1.6M เป็นระบบถามตอบเฉพาะเรื่องกะเพรา ตัวจัดหมวดคำถามใช้ Tiny Transformer ประมาณ 1.65 ล้านพารามิเตอร์ เพื่อเลือกหมวดคำตอบหรือแจ้งว่าไม่มีข้อมูล โครงการมีแพ็กเกจสำหรับทดลองบนพีซีและรันบน CPU ของบอร์ด ALINX AX7010

## ดาวน์โหลด

| แพ็กเกจ | เครื่องที่ใช้ | ไฟล์สำคัญ |
| --- | --- | --- |
| [KapraoTiny-1.6M.zip](https://github.com/mosccer/kapro-ai/raw/refs/heads/main/KapraoTiny-1.6M.zip) · 12.9 MB | พีซี ใช้ Python 3.10 ขึ้นไปและ PyTorch | `kaprao.py`, `kaprao_model.pt`, `kaprao_gen.pt`, ชุดข้อมูล และผลประเมิน |
| [KapraoTiny-1.6M-AX7010-CPU.zip](https://github.com/mosccer/kapro-ai/raw/refs/heads/main/KapraoTiny-1.6M-AX7010-CPU.zip) · 21.4 MB | ALINX AX7010 ใช้ CPU ARM Cortex-A9 และ Linux 32 บิต ARMv7 hard-float เช่น PetaLinux | โปรแกรม C++ ที่คอมไพล์แล้ว ไฟล์โมเดล FP32 และคู่มือ `README_AX7010.md` |

## รันบนพีซี Windows

แตก ZIP แล้วเปิด PowerShell ในโฟลเดอร์ที่มี `kaprao.py`

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe kaprao.py ask "ผัดกะเพราใส่อะไรบ้าง"
```

ถ้าต้องการถามต่อเนื่อง ให้รันคำสั่งโดยตัดข้อความคำถามท้ายบรรทัดออก พิมพ์ `exit` เพื่อจบ โปรแกรมรับคำถามเป็นรายครั้ง ตัวอย่างคำถามคือ “กะเพราต่างจากโหระพาอย่างไร” และ “ปลูกกะเพราอย่างไร” ดูคำสั่งฝึกและประเมินเพิ่มเติมใน `README.md` ภายใน ZIP

## รันบนบอร์ด ALINX AX7010

1. บูตบอร์ดด้วย Linux สำหรับ ARMv7 และเปิดเทอร์มินัลบนบอร์ด
2. แตก ZIP แล้วคัดลอกโฟลเดอร์แพ็กเกจไปยังระบบไฟล์ Linux บนบอร์ด
3. เข้าโฟลเดอร์ที่มี `bin/` และ `model/` แล้วรัน

```sh
chmod +x bin/kaprao_ax7010
./bin/kaprao_ax7010 --gen model/kaprao_gen_fp32.bin --ask "ผัดกะเพราใส่อะไรบ้าง"
```

แพ็กเกจนี้ใช้โปรแกรมที่รันบน CPU ของ Zynq-7010 และต้องบูต Linux ก่อน คำสั่งด้านบนใช้ไฟล์โมเดลที่ export สำหรับโปรแกรม C++ โดยตรง รายละเอียดการตั้งค่า Serial การคอมไพล์ และการแก้ปัญหาอยู่ใน `README_AX7010.md` ภายใน ZIP

## สถานะการตรวจสอบ

ไฟล์ ZIP บน GitHub ตรงกับแพ็กเกจต้นทางทั้งสองไฟล์ตาม Git blob SHA การอัปเดตคู่มือครั้งนี้ยังไม่ได้ทดสอบรันบนบอร์ดจริง
