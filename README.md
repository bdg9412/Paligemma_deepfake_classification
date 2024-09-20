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

## Methods
- Model
    - google/paligemma-3b-pt-224 (코랩 / L4에서 학습 진행)   
        - Gemma 중 multimodal 모델 선택  
- Data Processing
    - question 컬럼에 대하여 직접 생성 진행 (단순 질문 : step loss[0.135400] / 정보 추가 질문 : step loss[0.118300])  
    - question 컬럼에 심플한 정보 추가의 경우, step loss는 줄어들었지만 분류 능력은 하락  
      ㄴMM-CoT 관련 논문에서 LLM에 CoT를 추가하는 방식으로 접근하는 것은 성능 향상에 도움이 안되는 정보 확인  
    - MM-CoT 논문의 image feature 정보를 주는 것에 착안하여 image captioning 정보를 모델의 입력에 추가  
      ㄴ QLora의 r값을 증대시켜 표현력을 높이는 접근법과 프롬프트 구성 방안의 변경이 필요한 것을 확인  
      ㄴ 프롬프트 구성에 따라 step loss가 0.186500에서 0.136900까지 비교적 크게 변경되는 것을 확인  
     
## Reference
huggingface/transformers (https://github.com/huggingface/transformers)  
paligemma finetuning (https://github.com/merveenoyan/smol-vision)    
https://www.youtube.com/watch?v=iyYh4PQBI9U  
https://github.com/bdg9412/2024_Korean_CCI  
@misc{zhang2024multimodalchainofthoughtreasoninglanguage,
      title={Multimodal Chain-of-Thought Reasoning in Language Models}, 
      author={Zhuosheng Zhang and Aston Zhang and Mu Li and Hai Zhao and George Karypis and Alex Smola},
      year={2024},
      eprint={2302.00923},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2302.00923}, 
}
## License  
Gemma 2 License: https://ai.google.dev/gemma/terms  
