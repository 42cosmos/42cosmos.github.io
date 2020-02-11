---
layout: post
title: 'Seaborn Visualisation'
tags: [visualisation, Seaborn]
categories: [Study/Python]

---

### Bar Chart



#### DataFrame 형태로 반환

*데이터가 리스트 형태로 있음을 가정*

```python
def make_df(df1, df2, col1, col2, sort=True):
    df_name = pd.concat([pd.Series(df1), pd.Series(df2)], axis=1)
    df_name.columns = ['{}'.format(col1), '{}'.format(col2)]

    if sort is False:
        return df_name

    if sort is True:
        return df_name.sort_values(by=('{}'.format(col1)), ascending=False)
```

1. 리스트를 시리즈 형태로 만들어서 concat을 axis =1 로 맞추어 합쳤다. 두 개 이상 받을 때는 이 함수를 못쓰는데... 여러개 받게끔 할 수도 있지 않을까? 
2. 데이터는 Numeric type 이기 때문에 배열 정렬을 할 수 있어서 기본이 True인 선택값으로 넣어줬다. 





#### Bar Chart with Seaborn

*데이터가 데이터프레임 형태로 있음을 가정*

```python
def bar_plot(dataframe, font_size=11, grid=False):
    plt.figure(figsize=(10, 10))
    ax = sns.barplot(data=dataframe, x=dataframe.columns[1], y=dataframe.columns[0], palette='Blues')
    
    plt.rcParams["font.size"] = font_size
    plt.xlabel(dataframe.columns[1], fontsize=font_size+5)
    plt.ylabel(dataframe.columns[0], fontsize=font_size+5)

    if grid is True:
        ax.grid(axis='y')
        plot_value(ax, fontsize=font_size+1)
    else:
        plot_value(ax, fontsize=font_size+1)

    return ax
```

1. 들어온 데이터프레임은 sns.barplot으로 만들어준다. 여기서 x와 y는 df.columns[n]으로, 데이터프레임에서 특정 열을 뽑아 (시리즈) 지정해준다. 
2. 팔레트는 아무 색이나 넣어봤다
3.  [rcParams](https://financedata.github.io/posts/faq_matplotlib_default_chart_size.html) 으로 차트를 다양하게 만질 수 있다길래 폰트 사이즈를 바꿨다.   
   저렇게 말고 다르게 바꿀 수 있는 방법은 없나 고민을 하다가... 이미 바꿨는데 왜 또 대안을 찾나 싶어서 관뒀다.
4. 그리드 선택 기본값 False



#### Multiplt Bar Chart

```python
data = pd.melt(tmp2, id_vars=Zs[0], var_name="Brands", value_name="Counts (%)")

def multiple_bar_chart(data, ylim, ylabel_text="Count", font_size=11, figsize=(10,10)):
    plt.figure(figsize=figsize)
    mb = sns.barplot(x='labels', y='Counts (%)', hue='Brands', data=data,
                 palette='PRGn_r')

    sns.despine(fig=None, ax=None, top=False, right=False,
           left=False, bottom=False, offset=None, trim=False)
    plt.legend(loc='center left', bbox_to_anchor=(1,0.5), shadow=True, ncol=1, fontsize="large")
    plt.xlabel('')
    plt.ylabel(ylabel_text, fontsize=font_size+5)
    plt.ylim(0, ylim)
    plt.xticks(fontsize=font_size+3)
    plt.yticks(fontsize=font_size+3)

    plot_value(mb, fontsize=font_size+1)
```

1. 들어오는 data는 melt 함수를 적용한 df다. melt 함수에서 var_name과 value_name을 지정해주고 그걸 y와 hue로 지정해줬는데,... 다른 방법을 사용하면 함수 재활용을 할 수 있을 것 같다. y와 hue를 column으로 불러준다느니 뭐나느니 하면서... 
2. sns.despine은 barplot이 뚜껑이 휭 하길래 넣어줬더니 뚜껑이 만들어졌다. 정확히 이해를 못하고 집어 쳐넣은 거라 아직도 이해를 못했다.



### Display Values in Plot

ha와 va만 제대로 알고 있었어도 이렇게 개고생은 안 하는 건데 나는 바보 멍청이다.

시간을 오래 끌게 만든 내 무지함이 원망스러웠다. 

```python
def plot_value(ax, axis=0, fontsize=10):
    if axis == 0:
        for p in ax.patches:
            x = p.get_x() + p.get_width() / 2
            y = p.get_y() + p.get_height() * 1.01
            value = int(p.get_height())
            ax.text(x, y, value, ha="center", fontsize=fontsize) 

    elif axis == 1:
        for p in ax.patches:
            x = p.get_x() + p.get_width() * 1.01
            y = p.get_y() + p.get_height() / 2
            value = p.get_width()
            
            ha = 'left'

            if x < 0:
                ha = 'right'
                
            plt.text(x, y, value, va='center', ha=ha, fontsize=fontsize)
```

1. axis=0일 때, 즉 세로형 그래프일 때는 음수값이 하나도 없었으니까 버무리고 넘어갈 수 있었다. 
   1. [ax.patches](https://dailyheumsi.tistory.com/98)로 막대기를 하나씩 끌어오고, 각 막대기가 갖고 있는 값을 p.get_sth()으로 가져온다. 가져올 수 있는 값은 4개로, left(x), bottom(y), width, height 이다. 
   2. x은 그래프 최상단의 값을 정중앙에 놓기 위해 막대기의 절반 값을 만들어주고, y는 그 값을 막대기와 값 사이의 여백을 주어 가독성을 높이기 위해 설정 해주었다. value 설정을 안 해주고 그냥 height 값을 집어넣으면 float 타입으로 반환 된다. 내 기준에 소수점은 안 예뻐서 int 값으로 때려박았다. 
2. axis=1 == 가로형 그래프
   1. ha와 va의 용법이 문제였다!!!! 우ㅇ아아아



### Pandas from_records & melt Function

데이터 재구조화   

*a, b값은 리스트*

```python
def from_records(a, b, columns):
    tmp = pd.DataFrame.from_records(
        [('comments', a[0], a[1], a[2], a[3]), ('likes', b[0], b[1], b[2], b[3])], columns=columns)
    return pd.melt(tmp, id_vars=columns[0], var_name="source", value_name="value_numbers")
```

이것도 저 a[0]~ 이 부분을 어떻게 바꿀 수 있지 않을까 생각이 드는데 ... ㅠㅠ 흠 

https://rfriend.tistory.com/tag/Python%20pandas%20melt%28%29%20함수

이 블로그가 설명을 아주 기깔나게 잘 해주셔서 많이 참고했다.



### Seaborn catplot

```python
def catplot(input_df, value=0.1, font_size=11):
    sns.set_style("white")
    a = sns.catplot(
        x="value_numbers", y="source", hue="labels", data=input_df, kind="bar", orient='h', legend=False)
    plt.xlim(-value, value)
    plt.legend(loc='center left', bbox_to_anchor=(1,0.5), shadow=True, ncol=1)
    sns.despine(fig=None, ax=None, top=False, right=False, left=False, bottom=False, offset=None, trim=False)
    a.fig.set_size_inches(15,15)
    a.set_xlabels('')
    a.set_ylabels('')
    plt.xticks(fontsize=font_size+3)
    plt.yticks(fontsize=font_size+3)

    plot_value(a.ax, axis=1, fontsize=font_size+1)
```

Col 별로 x, y 데이터를 보여줄 수 있다. 

sns.catplot 내부에서 legend를 False 처리하고 바깥에서 matplotlib 으로 처리해줬다. 



참고 : https://stackoverflow.com/questions/38807895/seaborn-multiple-barplots

### Frequency Distribution

*데이터가 csv 파일 형태로 있음을 가정*

``` python
def frequency_distribution(df_col, max_limit, fontsize=15):
    
    mean = df_col.mean()
    stddev = df_col.std()
    number = df_col.shape[0]
    
    f,ax1 = plt.subplots(figsize=(10, 10))
    sns.distplot(df_col,kde=False,ax=ax1)
    plt.xlim(-(max_limit*0.05), max_limit)
    plt.xlabel(df_col.name, fontsize=fontsize)
    plt.ylabel('Frequency', fontsize=fontsize)
    ax2 = ax1.twinx()
    
    inbox = "Normal\nMean = %0.2f\nStd. Dev. = %0.2f \nN = %s" %(mean, stddev, number)
    textbox = offsetbox.AnchoredText(inbox, loc=1)
    ax2.add_artist(textbox)

    sns.distplot(df_col, hist=True, kde=False, fit=norm, ax=ax2)
    ax2.yaxis.set_ticks([])
```





### 고찰

뭔가 더 좋은 방법이 있지 않을까 항상 고민을 하지만... 능력이 없어 고민으로 시간을 질질 끌다 결국 막을 내리기만 해 답답하기만 하다.

빈도수 차트는 왜 선이 꾸깃꾸깃하게 나올까 미치겠다... 

다 하고 교수님 메일이 아니라 깃허브로 보냈고 교수님이 머지해 주시긴 하셨는데... 생각해보니 메일로 보냈어야 하나 싶다... ㅠㅠ아니 선이 왜 꾸깃꾸깃 하냐고 진짜 미치겠네

ㅇ