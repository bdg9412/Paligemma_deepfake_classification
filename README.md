# Paligemma_deepfake_classification
본 리포지토리는 [2024 Aifactory Geema hackathon](https://aifactory.space/task/2733/overview) 아이디어 기획에 대한 구현 소스 코드를 포함하고 있습니다.

## 경진대회 결과
- 대상 수상🏆  
![image](https://github.com/user-attachments/assets/91bbaeac-75c2-4fa5-bd94-031ed78e6a5a)

## Purpose  
- 생성형 AI 모델을 딥페이크 이미지 분류에 특화되도록 파인튜닝 수행  

## Data Format
```
{
    "image": "deepfake image or normal imgae",
    "label": "0(deepfake image) / 1(normal image)"
    "question": "Is this image made by AI?"
}
```
## Key Point
- MultiModal 모델 활용
- QLora 적용

## Methods
- Model
    - google/paligemma-3b-pt-224 (코랩 / L4에서 학습 진행)   
        - Gemma 중 이미지와 텍스트를 함께 입력으로 사용할 수 있는 multimodal 모델 선택  
- Data Processing
    - question 컬럼에 대하여 직접 생성 진행
      - 단순 질문 : step loss[0.135400] / 정보 추가 질문 : step loss[0.118300] 
    - question 컬럼에 심플한 정보 추가의 경우, step loss는 줄어들었지만 분류 능력은 하락  
      - MM-CoT 관련 논문에서 LLM에 CoT를 추가하는 방식의 접근 법은 성능 향상에 도움이 안되는 정보 확인  
    - MM-CoT 논문의 image feature 정보를 주는 것에 착안하여 image captioning 정보를 모델의 입력에 추가  
      - QLora의 r값을 증대시켜 표현력을 높이는 접근법과 프롬프트 구성 방안의 변경이 필요한 것을 확인  
      - 프롬프트 구성에 따라 step loss가 0.186500에서 0.136900까지 비교적 크게 변경되는 것을 확인

## Results  
- Paligemma를 활용하여 Deepfake 이미지 분류 모델 학습 및 추론 진행  
  - 0 (deepfake 이미지) / 1 (normal 이미지) 분류 확인 완료 (https://github.com/bdg9412/Paligemma_deepfake_classification/blob/main/Fine_tuned_Model_Inference_202409.ipynb)
  - 10 epoch 학습 이후 1000개 이미지 대상 accuracy 측정 결과 : 94.80 (label 분포 : {0: 541, 1: 459})  
   

     
## Reference
huggingface/transformers (https://github.com/huggingface/transformers)  
paligemma finetuning (https://github.com/merveenoyan/smol-vision)   
Zhang, Z., Zhang, A., Li, M., Zhao, H., Karypis, G., & Smola, A. (n.d.). Multimodal Chain-of-Thought reasoning in language models. (https://arxiv.org/abs/2302.00923)  

## License  
Gemma 2 License: https://ai.google.dev/gemma/terms  
