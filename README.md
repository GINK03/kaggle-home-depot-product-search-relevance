# kaggle-home-depot-product-search-relevance

## 言語と関連のランキング表現

## ランキングはRMSEで評価している

## 最も基礎的な観点は、関連度でランキングを表現する

```python
# str2の中にstr1の単語が何回出現するかみたいな
def str_common_word(str1, str2):
        return sum(int(str2.find(word)>=0) for word in str1.split())
        
df_all['search_term']         = df_all['search_term'].map(lambda x:str_stemmer(x))
df_all['product_title']       = df_all['product_title'].map(lambda x:str_stemmer(x))
df_all['product_description'] = df_all['product_description'].map(lambda x:str_stemmer(x))
df_all['len_of_query']        = df_all['search_term'].map(lambda x:len(x.split())).astype(np.int64)
df_all['product_info']        = df_all['search_term']+"\t"+df_all['product_title']+"\t"+df_all['product_description']

# タイトルで何回マッチしたか
df_all['word_in_title']       = df_all['product_info'].map(lambda x:str_common_word(x.split('\t')[0],x.split('\t')[1]))
# デスクリプションで何回マッチしたか
df_all['word_in_description'] = df_all['product_info'].map(lambda x:str_common_word(x.split('\t')[0],x.split('\t')[2]))

df_all = df_all.drop(['search_term','product_title','product_description','product_info'],axis=1)
```
