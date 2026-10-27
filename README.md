# Live2D From Image

Một ảnh nhân vật anime (hoặc một PSD đã tách layer) → model 2D cử động được: quay đầu, chớp mắt, thở, nhìn theo
chuột, tóc / váy / ngực / tay / chân có vật lý, kèm motion và biểu cảm. Xuất thẳng sang **Live2D**
(`.model3.json` + `.moc3`, mở được bằng VTube Studio) và **`.p2lrt`** (runtime PSD2Live).

Không cần Cubism Editor, không cần biết rig.

Repo này chỉ chứa **bộ cài** và ghi chú từng phiên bản. Xem mục [Releases](../../releases) để tải.

## Tải và cài

1. Vào [bản mới nhất](../../releases/latest), tải `Live2D-From-Image-Setup-<phiên bản>.exe` rồi chạy.
2. Windows có thể hiện "Windows protected your PC" vì bộ cài chưa ký số: bấm **More info → Run anyway**.

- Chỉ hỗ trợ **Windows 10/11 64-bit**.
- **App tự cập nhật**: khi có bản mới, app tự tải về và thanh tiêu đề hiện nút **"Khởi động lại để cập nhật"**.
  Không cần tải lại bộ cài.

## Bắt đầu nhanh

1. **＋ Tạo mới ▾** → **Từ ảnh (See-through)** → chọn ảnh. Ảnh tốt nhất: nhân vật nhìn thẳng, thấy rõ mặt, cả
   người, nền đơn giản.
2. Chờ app tách layer và dựng model. Bấm **▶ Chạy tiếp** trên thanh nhanh nếu app dừng chờ bạn xem lại.
3. Xem model ở khung bên phải:
   - Kéo để di chuyển, lăn chuột để phóng to, nhấp đúp để căn giữa.
   - Bật "Nhìn theo chuột", bấm thử các nút motion và biểu cảm.
4. Chỉnh cảm giác chuyển động ở tab **Chỉnh & xuất** → **Tinh chỉnh chuyển động** (tóc, váy, ngực, tay, chân…).
   - Bấm ▶ cạnh một thông số để xem ngay hiệu ứng của nó.
   - Ô tìm kiếm giúp tìm nhanh thông số.
   - ↶ ↷ để hoàn tác và làm lại.
   - Lưu bộ thông số ưng ý để dùng lại cho model sau.
5. Đặt **Tên model** → **⇪ Xuất Live2D…** → chọn thư mục, ví dụ thư mục `Live2DModels` của VTube Studio.

Các job được lưu ở `Documents/Live2DFromImage/generations/`.

## Có cần cài See-through không?

**Không.** Mặc định app gọi See-through trên Hugging Face, không phải cài thêm gì.

- **Nên có Hugging Face token**: tạo miễn phí ở huggingface.co → Settings → Access Tokens (quyền `read`), rồi dán
  vào hộp ⚙ See-through. Không có token, hạn mức GPU miễn phí dùng chung rất nhanh hết và app sẽ báo "Hết hạn mức
  GPU". Token được lưu mã hoá bằng Windows.
- **Chạy trên Google Colab** (miễn phí, không cần GPU riêng): trong hộp ⚙ See-through, bấm "Lưu notebook & mở
  Colab". Trên Colab chỉ cần Tải lên → Chạy tất cả → chọn ảnh, rồi đưa PSD kết quả về app.
- **Chạy trên máy mình**: tuỳ chọn, cho máy có GPU NVIDIA. Cần tự cài
  [See-through](https://github.com/shitagaki-lab/see-through) theo hướng dẫn của nó. GPU dưới 8 GB thì bật "GPU
  dưới 8 GB": chạy được trên 4 GB nhưng mất 40–90 phút mỗi ảnh.
- **Đã có PSD tách layer** (vẽ tay hoặc từ tool khác)? Dùng **Từ file PSD**: không gọi AI, không cần token, xong
  trong vài giây. Cách app đọc tên layer có ở mục [Đặt tên layer trong PSD](#đặt-tên-layer-trong-psd) bên dưới.

## Layer tách sai? Sửa ngay trong app

Chọn layer trong danh sách **Layer** rồi tô bằng cọ:

- **Tẩy**: bỏ phần vẽ lố.
- **Chuyển sang**: đưa phần tô sang layer khác, ví dụ tách váy khỏi áo.
- **Vẽ bù AI**: vẽ thêm phần bị che.
- **Tô màu**: tô thẳng màu lên layer.

Có hoàn tác, và các lần sửa được giữ khi đọc lại PSD.

Muốn chuyển động chi tiết hơn thì tách riêng các phần sau. Mỗi phần có chuyển động riêng:

| Tách sang | Dùng cho |
|---|---|
| **Tóc mai** | lọn tóc dài rủ cạnh mặt |
| **Đuôi tóc** | tóc đuôi ngựa, tóc buộc hai bên |
| **Áo ngoài** | áo khoác, áo choàng |
| **Phụ kiện trên áo** | mặt dây, xích, nơ thả |
| **Phụ kiện váy** | đuôi, ruy băng, nơ thả từ váy |

## Kiểm tra model trước khi xuất

- **Kiểm khe hở**: cho model đi qua các tư thế cực (quay, nghiêng đầu, xoay thân, lắc hông, vung tay…) và tô hồng
  chỗ lộ nền. Mỗi tư thế có ảnh minh hoạ, và nút "Giữ tư thế này" để xem kỹ.
- **⇄ So với bản trước**: sau khi đổi thông số và dựng lại, bấm để xem lại bản cũ cạnh bản mới.

## Model có gì

| Nhóm | Có gì |
|---|---|
| Đầu, thân | quay / ngẩng / nghiêng đầu, xoay thân, thở, thân xoay theo đầu |
| Mặt | mở / nhắm mắt, mắt cười, nhìn theo, lông mày, miệng mở và nói a-i-u-e-o, má hồng |
| Vật lý | tóc mái, tóc sau, tóc mai, đuôi tóc, phụ kiện tóc, tai thú, ngực, váy và phụ kiện váy, tay, chân |
| Chân | khuỵu gối, lắc hông, nhấc chân, đưa chân ra |
| Motion | Idle, Idle 2, Nhún nhảy, Lắc hông, Gật đầu, Lắc đầu, Nghiêng đầu, Vui, Ngạc nhiên, Buồn, Ngượng, Suy nghĩ, Ngáp, Nói a-i-u-e-o |
| Biểu cảm | Cười, Buồn, Giận, Ngạc nhiên, Ngượng, Nháy mắt |

Tên và biên độ thông số theo chuẩn Live2D (`ParamAngleX`, `ParamEyeLOpen`, `ParamMouthOpenY`…). Nhờ vậy VTube Studio
và các app dùng pixi-live2d-display điều khiển được ngay mà mặt không méo.

## Đặt tên layer trong PSD

App đọc **tên layer** để biết layer nào là gì. Tên không phân biệt hoa thường; dấu cách, gạch ngang, gạch dưới và
hậu tố kiểu "copy 2" đều được bỏ qua. Trái / phải là **của nhân vật**: tai trái nằm bên phải ảnh. File đặt theo phía
người xem cũng được nhận ra và đổi lại.

| Bộ phận | Tên nhận ra (ví dụ) |
|---|---|
| Tóc | `front hair`, `bangs`, `前髪` · `back hair`, `後髪` · `side hair l/r` · `ponytail`, `twin tails` |
| Phụ kiện đầu | `hair accessory`, `headwear`, `hat`, `ribbon`, `glasses` |
| Mặt | `face`, `skin`, `顔` · `nose` · `blush` · `ear l/r` |
| Mắt | `eye white l/r` · `iris l/r` · `highlight l/r` · `eyelash l/r` · `eyebrow l/r` · `closed eye l/r` |
| Miệng | `mouth`, `lips` · `mouth inner`, `teeth` |
| Thân | `neck` · `body`, `torso` · `arm l/r` · `hand l/r` · `legs`, `legwear`, `shoes` |
| Trang phục | `clothes top`, `topwear`, `dress` · `collar`, `scarf` · `skirt`, `bottomwear` · `skirt ribbon` |
| Khác | `accessory`, `bag`, `weapon`, `wings`, `tail` |

- Thứ tự vẽ lấy theo file. Layer ẩn bị bỏ qua. Group được làm phẳng; clipping layer, mask và opacity được giữ.
- Phần bị che (mặt dưới tóc mái, cổ dưới áo) nên vẽ đủ. Nếu thiếu, app tự kéo dài mép xuống dưới.

## Gặp lỗi?

Mở [Issues](../../issues) và gửi kèm:
- phiên bản app (ở thanh tiêu đề),
- bạn đang làm bước nào,
- ảnh chụp màn hình.

**Đừng đính kèm ảnh hay PSD bạn không có quyền chia sẻ.** Issue ở đây ai cũng xem được.

## Bản quyền

Model bạn tạo ra từ ảnh của mình là của bạn. Quyền với **ảnh gốc** vẫn thuộc người vẽ. Hãy chỉ dùng ảnh bạn được
phép dùng. App dùng các thành phần bên thứ ba (runtime PSD2Live, một số gói npm; See-through chạy trên Hugging Face, Colab
hoặc máy bạn chứ không đóng gói kèm app). Mỗi thành phần giữ giấy phép riêng của nó.
