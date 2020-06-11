# Model
Đây là nơi nhóm sinh viên dùng để tạo model machine translation

Để chạy mô hình nhóm sinh viên phát triển yêu cầu cần có:
 - Python3
 - Tensorflow 1.x (tốt nhất là 1.15)

Cách cài đặt:
- Đầu tiên cần tải repo từ github về máy bằng lệnh: https://github.com/nmtri1912/Model.git

- Sau đó ta cần tạo 3 folder trống:
     * word_embedding: nơi chứa pre-trained từ nhúng dành cho 2 ngôn ngữ tiếng Anh và tiếng Việt.
     * vocab_english: nơi sẽ chứa tập tin word2int và int2word tiếng Anh được tạo ra trong quá trình training.
     * vocab_vietnamese: nơi sẽ chứa tập tin word2int và int2word tiếng Việt được tạo ra trong quá trình training.

- Ta sẽ có cây thư mục như hình:

<div align="center">
       <img src="/imgs/foldertree.png" width="300px" height="300px"</img>
</div>
     
- Sau khi thực hiện các bước trên để training mô hình từ đầu ra chạy lệnh:
  <div>
  <pre>
    !python3 train.py 
      --language_src data/train-en-vi/train.en 
      --language_targ data/train-en-vi/train.vi 
      --vocab_src vocab_english/ 
      --vocab_targ vocab_vietnamese/ 
      --word_emb_src word_embedding/model_en.bin 
      --word_emb_targ word_embedding/model_vn.bin  
      --num_layer 1 
      --num_hiddens 512 
      --learning_rate 0.001 
      --keep_prob 0.85 
      --beam_width 10 
      --batch_size 64  
      --checkpoint NMT.ckpt
  </pre>
  </div>
Các tham số trên chỉ là tham khảo, ta có thể tùy chỉnh.

- Sau khi chạy xong ta sẽ có được file checkpoint sau mỗi epoch:
<div align="center">
       <img src="/imgs/checkpoint.png" width="300px" height="300"</img>
</div>

- Nếu muốn train tiếp với checkpoint được lưu ta chạy đoạn lệnh:
  <div>
  <pre>
    !python3 train_load.py 
      --language_src data/train-en-vi/train.en 
      --language_targ data/train-en-vi/train.vi 
      --vocab_src vocab_english/ 
      --vocab_targ vocab_vietnamese/ 
      --word_emb_src word_embedding/model_en.bin 
      --word_emb_targ word_embedding/model_vn.bin  
      --num_layer 1 
      --num_hiddens 512 
      --learning_rate 0.001 
      --keep_prob 0.85 
      --beam_width 10 
      --batch_size 64  
      --checkpoint NMT.ckpt
  </pre>
  </div>

- Để thực hiện dịch một file từ tiếng Anh sang tiếng Việt ta chạy đoạn lệnh:
