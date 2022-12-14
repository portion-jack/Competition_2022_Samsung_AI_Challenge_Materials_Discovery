## 2022 Samsung AI Challenge (Materials Discovery)
### (2022.08.08 ~ 2022.09.16 11:59)
### 주제 : 유기분자 구조로부터 Reorganization Energy를 예측하는 AI 알고리즘 개발

### 1차 시도
- mol file을 read_line 을 통해 parsing
-   - 구조에 따라 원자좌표, 원자 결합 종류등을 파악한다.
- 이를 array 형태로 broadcasting 데이터의 크기는 제일 큰것을 기준으로 맞춘다
-   - 이후 tensorflow를 통해 회귀 분석진행

    ```
    유의미한 결과는 아닌듯 하다.
    ```


### 2차 시도
(mol_file에서 무언가를 얻어내는것 보다는 smiles을 활용하는것이 상당히 높은 가능성을 가지는것 같다.)
1. data
	1.1 SMILES 
		- NLP 처리 하여 tensor형태로 변환

2. modeling
	2.1 tensor -> GRU

# (15/450) with acc = 15.1

### 1차 시도
1. data
    - 1.1 SMILES (분자구조식)
		- 1.1.1 SMILES files -> to some tensor
			-> by rdkit (reference to 2021 Competition)
    - 1.2 .mol 파일 (status={ex,g}) 
        - 1.2.1 atom 개수 bond 개수 -> done
        - 1.2.2 atom들의 location, element_type (x,y,z,element_type) -> done
        - 1.2.3 bond결합 atom구조, (atom_1,atom_2,bond_type) -> done

2. modeling
	- (,2) :mol -> count
	- (,4) :mol -> location
	- (,3) :mol ->  bond
	- (,2048) : SMILES -> tensor
		- keras
		- input shape (,2) (,4) (,3) (,2048)

keras모듈로 GRU를 사용하여 답안 제시
개인으로 참여하여
213개의 팀중 17위

<img width="1098" alt="image" src="https://user-images.githubusercontent.com/112222918/202943257-375fe0b3-77a9-4def-8f23-785cf2760992.png">



