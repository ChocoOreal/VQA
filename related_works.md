## [VQAR: Review on Information Retrieval Techniques based on Computer Vision and Natural Language Processing](./modi2019.pdf)
Một framework của VQA gồm có:
* Câu hỏi
    - Trích xuất hình ảnh
    - Trích xuất ngôn ngữ
* Kết hợp 
* Phương pháp VQA
    - Joint embedding
    - Attention machanism: chỉ tập trung vào một khu vực của ảnh thay vì toàn bộ hình ảnh. Các khu vực trong bức ảnh sẽ được đánh trọng số, thể hiện tầm quan trọng.
    - Compositional model: lý luận nhiều bước (multi-step reasoning). Ví dụ "what is left to the dog", model sẽ tìm con chó trước, sau đó tìm phía bên trái của con chó. -> Mô hình có hai thành phần.
    - External knowledge base machanism: Cần thêm các kiến thức bên ngoài để trả lời câu hỏi
* Dự đoán
* Trả về kết quả

### Kỹ thuật được sử dụng
#### [Stacked attention network (SAN)](./Yang_Stacked_Attention_Networks_CVPR_2016_paper.pdf) 
Dựa vào attention machanism, lý luận nhiều bước (multi-step reasoning) thông qua nhiều lớp attention, gồm 3 thành phần chính:
* Trích xuất hình ảnh (VGGnet CNN)
* Trích xuất câu hỏi (CNN, LSTM)
* Stacked attention model: Tìm những khu vực quan trọng trong hình.

Cuối cùng kết hợp đặc trưng thu được từ lớp attention cuối cùng và vector query cuối cùng để dự đoán kq. Kết quả dc trả về là một câu.

Các loại câu hỏi: object, color, count and location.

#### [ABC-CNN](./1511.05960.pdf)
Mô hình CNN dựa vào attention machanism. Tập trung vào một khu vực trong ảnh dựa vào question guided attention. Gồm 4 thành phần: 
* Image feature extraction: VGG-19 deep-CNN
* Question feature extraction: LSTM
* Attention extraction: dùng convolutional kernels, giúp ánh xạ question features với image features để tạo question guided attention map. 
* Answer generation: dựa vào question guided attention map.

Kết quả trả về là một câu.

Các loại câu hỏi: object, color, count and location.

#### [Learning Conditioned Graph Structures](./1806.07243.pdf)
Dựa vào cơ chế attention. Tạo một graph dựa vào ảnh đầu vào có liên quan đến câu hỏi. Nhờ vậy mà đạt được lý luận cấp độ cao (high level reasoning) như là ngữ nghĩa (semantic) và biểu diễn trong không gian (spatial representations). Gồm 4 thành phần:
* Question encoder: word embedding, RNN. 
* Object detector: tìm tọa độ của bounding box và feature vector của ảnh. 
* Graph learner module: kết hợp feature vector của ảnh và câu hỏi, tạo adjacency matrix cho image objects và câu hỏi đã cho. 
* Spatial graph convolution: tập trung vào object, các quan hệ đối với object và có tầm ảnh hưởng cho việc trả lời câu hỏi. 


Cuối cùng ta áp vào max-pool và nhân từng phân tử để tìm ra câu trả lời. Trả lời dc các câu hỏi về thời gian (time specific question), trả lời tốt các câu hỏi về số lượng.

Object, color, count
#### [Learning to Reason: Endto-End Module Networks](./1704.05526.pdf)
Kết hợp cơ chế attenction và compositional model. Phân tách câu hỏi thành các neural modules riêng biệt. 

#### [R-VQA](./1805.09701.pdf)
Mỗi data trong tập R-VQA bao gồm ảnh, câu hỏi, relation fact (được tạo ra từ relation detector từ ảnh và câu hỏi)và câu trả lời. Mô hình gồm 3 thành phần: 
* Context aware visual attention
* Fact aware semantic attention (KQ trả ra của tp 1 sẽ được feed cho tp2 để chọn ra những relation facts liên quan)
* Joint knowledge embedding learning: kết hợp visual và semantic attention để học kiến thức hình ảnh và ngữ nghĩa. 

Trả lời trong nhiều từ. 

Dạng câu hỏi: Object, color, activity, position, scene, relation, commonsense

### Các vấn đề còn tồn tại
[SAN](./Yang_Stacked_Attention_Networks_CVPR_2016_paper.pdf) và [ABC-CNN](./1511.05960.pdf) chỉ trả lời được trong 1 từ, trong nhiều trường hợp gây khó khăn cho con người.

