# Paligemma_deepfake_classification
본 리포지토리는 [2024 Aifactory Geema hackathon](https://aifactory.space/task/2733/overview) 아이디어 기획에 대한 구현 소스 코드를 포함하고 있습니다.

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
- CoT(Chain-of-Thought) 적용

## Methods
- Model
    - [google/paligemma-3b-pt-224 (코랩 / L4에서 학습 진행)]  
        - Gemma 중 multimodal 모델 선택  
- Data Processing
    - question 컬럼에 대하여 직접 생성 진행 (단순 질문 : step loss[135400] / 정보 추가 질문 : step )
     
## Reference
huggingface/transformers (https://github.com/huggingface/transformers)  
https://github.com/merveenoyan/smol-vision  
https://www.youtube.com/watch?v=iyYh4PQBI9U  
https://github.com/bdg9412/2024_Korean_CCI  

## License  
Gemma 2 License: https://ai.google.dev/gemma/terms  
