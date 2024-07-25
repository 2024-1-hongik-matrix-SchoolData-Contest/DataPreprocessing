import pandas as pd

num = [19, 20, 21, 22, 23]
dfs = {}
df2019=pd.read_excel("/content/★2019~2023 학교안전사고 데이터_수정.xlsx", header=0, sheet_name='2019')
institutes = df2019['교육청'].unique()

# 데이터 로드
for i in num:
    dfs['df20{}'.format(i)] = pd.read_excel("/content/★2019~2023 학교안전사고 데이터_수정.xlsx", header=0, sheet_name='20'+str(i))

    for institute in institutes:
        score_column_name = 'df20{}_{}_score'.format(i, institute)
        dfs[score_column_name] = 0

        cond = dfs['df20{}'.format(i)]['교육청'] == institute
        injuries = ['머리(두부)', '치아(구강)', '흉복부', '팔', '다리', '손', '발', '기타']
        scores = [1.87, 0.13, 1.25, 0.15, 0.15, 0.15, 0.15, 0.33]

        for index, row in dfs['df20{}'.format(i)][cond].iterrows():
            injury_type = row.iloc[13]

            # 사고부위에 따른 점수 계산
            for j in range(len(injuries)):
                if injury_type == injuries[j]:
                    dfs[score_column_name] += scores[j]

# 각 연도별 교육청 별 점수 차이 계산
for k in range(len(num) - 1):
    current_year = num[k]
    next_year = num[k + 1]
    
    for institute in institutes:
        current_score_column = 'df20{}_{}_score'.format(current_year, institute)
        next_score_column = 'df20{}_{}_score'.format(next_year, institute)
        
        score_difference = dfs[current_score_column] - dfs[next_score_column]
        
        print('20{}_{}_개선점수= '.format(next_year, institute) + str(score_difference) + '\n')
