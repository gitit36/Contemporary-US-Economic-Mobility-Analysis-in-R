# Data-Science-report

***Principles of Data Science from a Statistical Point of View*** 

***ISP 2019*** 

***Professor Sungkyu Jung*** 

**Part I**
Fivethirtyeight data graphics An R package that provides access to the code and data sets published by FiveThirtyEight https://github.com/fivethirtyeight/data, was just made available to public. The developers, Albert Kim and his colleagues, maintains a webpage for the package fivethirtyeight: https://rudeboybert.github.io/fivethirtyeight/ 

The data sets included are massive. You can find a list of these, including the URLs to the original fivethirtyeight.com articles, at https://rudeboybert.github.io/fivethirtyeight/articles/fivethirtyeight.html. The task (Part I) is to choose one of the articles with data graphics, and recreate one or more of the data graphics found in the article. Examples of such report can be found at https://rudeboybert.github.io/fivethirtyeight/articles/ 

**The report will consist of**
1. A technical discussion of your data wrangling-visualization statements; 
2. A brief paragraph explaining the context of the data graphic you created, and be prepared by R markdown.   

**Part II. Retreive, explore, and analyze**
This part of the task is to retreive, explore, and analyze data in one of the topic areas. You will need to choose one from American Time Use Survey Data and Economic Mobility data (see below). 

**Scope of the work The final product will consist of**
1. visualization or tabulation of the data (from either exploring or modeling), 
2. results of statistic tests for your hypothesis, 
3. and modeling and predictions from statistical learning methods.  

**Report**
The report consists of 
1. Proposed goals in your progress report, 
2. Analysis (both code chunks and results), 
3. Interpretation,  

**Economic Mobility data**
We will look at economic mobility across generations in the contemporary USA. The data come from a large study1, based on tax records, which allowed researchers to link the income of adults to the income of their parents several decades previously. For privacy reasons, we don’t have that individual-level data, but we do have aggregate statistics about economic mobility for several hundred communities, containing most of the American population, and covariate information about those communities. We are interested in predicting economic mobility from the characteristics of communities. 
Data can be read using the following R code. There are 741 communities (observations) and 43 variables. 
dat &lt;- read.csv("mobility.csv")  

The variable we want to predict is economic mobility; the rest are predictor variables or covariates. 

1. Mobility: The probability that a child born in 1980–1982 into the lowest quintile (20%) of household income will be in the top quintile at age 30. Individuals are assigned to the community they grew up in, not the one they were in as adults. (가계 소득의 최저 5 분위수 (20 %)에 속해 있는 1980-1982 년 출생한 아이가 30세에 되었을 때 상위 1 분위에 속할 확률)  

2. Population in 2000. (2000년 기준 인구)  

3. Is the community primarily urban or rural? (커뮤니티가 도시인가 시골인가?)  

4. Black: percentage of individuals who marked black (and nothing else) on census forms. (흑인의 비율)  

5. Racial segregation: a measure of residential segregation by race. (인종별 주거지 분리의 정도)  

6. Income segregation: Similarly but for income. (소득별 주거지 분리의 정도)  

7. Segregation of poverty: Specifically a measure of residential segregation for those in the bottom quarter of the national income distribution. (저소득층과 중상류층의 주거지 분리의 정도)  

8. Segregation of affluence: Residential segregation for those in the top qarter. (상류층과 중하층의 주거지 분리의 정도)  

9. Commute: Fraction of workers with a commute of less than 15 minutes. (15 분 미만 통근하는 주민의 비율)  

10. Mean income: Average income per capita in 2000. (평균 소득 )  

11. Gini: A measure of income inequality, which would be 0 if all incomes were perfectly equal, and tends towards 100 as all the income is concentrated among the richest individuals. ( 지니 계수)  

12. Share 1%: Share of the total income of a community going to its richest 1%. (상위 1% 가 차지하는 수입의 비율)  

13. Gini bottom 99%: Gini coefficient among the lower 99% of that community. (상위 1 %를 제외한 나머지의 지니 계수)  

14. Fraction middle class: Fraction of parents whose income is between the national 25th and 75th percentiles. ( 중산층 비율 )  

15. Local tax rate: Fraction of all income going to local taxes. ( 지방세율 )  

16. Local government spending: per capita. ( 1 인당 지방정부 지출 )  

17. Progressivity: Measure of how much state income tax rates increase with income. ( 세금 가중의 정도 )  

18. EITC: Measure of how much the state contributed to the Earned Income Tax Credit (a sort of negative income tax for very low-paid wage earners). ( 저소득층을 위한 세금 공제의 정도 )  

19. School expenditures: Average spending per pupil in public schools. ( 공립학교의 학생 1 인당 평균 지출. )  

20. Student/teacher ratio: Number of students in public schools divided by number of teachers.( 학생 / 교사 비율 )  

21. Test scores: Residuals from a linear regression of mean math and English test scores on household income per capita. ( 시험 점수: 언어+수학 점수를 평균 가정 소득에 회귀한 잔차 )  

22. High school dropout rate: Also, residuals from a linear regression of the dropout rate on per-capita income. ( 고등학교 중퇴율 : 실제 중퇴율를 평균 가정 소득에 회귀한 잔차 )  

23. Colleges per capita ( 1 인당 대학의 갯수 )  

24. College tuition: in-state, for full-time students ( 대학 등록금 )  

25. College graduation rate: Again, residuals from a linear regression of the actual graduation rate on household income per capita. ( 대학 졸업율: 실제 졸업율를 평균 가정 소득에 회귀한 잔차 )  

26. Labor force participation: Fraction of adults in the workforce. ( 노동인구 중 성인의 비율 )  

27. Manufacturing: Fraction of workers in manufacturing. ( 제조업 근로자의 비율 )  

28. Chinese imports: Growth rate in imports from China per worker between 1990 and 2000. ( 중국산 수입 증가율 )  

29. Teenage labor: fraction of those age 14–16 who were in the labor force. ( 노동인구 중 10 대의 비율 )  

30. Migration in: Migration into the community from elsewhere, as a fraction of 2000 population. ( 이사오는 비율 )  

31. Migration out: Ditto for migration into other communities. ( 이사 나가는 비율 )  

32. Foreign: fraction of residents born outside the US. ( 외국 태생 인구 비율 )  

33. Social capital: Index combining voter turnout, participation in the census, and participation in community organizations. ( 사회 참여의 정도 )  

34. Religious: Share of the population claiming to belong to an organized religious body. ( 종교 생활 참여의 정도 )  

35. Violent crime: Arrests per person per year for violent crimes. ( 폭력 범죄율 )  

36. Single motherhood: Number of single female households with children divided by the total number of households with children. ( 전체 아이가 있는 가정 중 엄마 혼자 아이 키우는 집의 비율 )  

37. Divorced: Fraction of adults who are divorced. (이혼한 비율 )  

38. Married: Ditto. ( 결혼한 비율 )  

39. Longitude: Geographic coordinate for the center of the community (경도: 동서 )  

40. Latitude: Ditto ( 위도: 남북 )  

41. ID: A numerical code, identifying the community. ( 커뮤니티 식별 코드 )  

42. Name: the name of principal city or town. ( 동네 이름 )  

43. State: the state of the principal city or town of the community. ( 동네가 속한 미국의 주)   

1. Chetty, Raj, Nathaniel Hendren, Patrick Kline and Emmanuel Saez (2014). “Where is the Land of Opportunity? The Geography of Intergenerational Mobility in the United States.” Quarterly Journal of Economics, 129: 1553– 1623. Finding and reading this paper does not actually help you↩ 
