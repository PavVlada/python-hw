# python-hw
### 1 пример
Проект в вузе с одногруппниками  
Ссылка на репозиторий (проектный):   
https://gitlab.com/theyoungggod/news_classifier/-/tree/main  

Писала код, который "разрезает" статью на куски (заданное количество предложений), а после проверяет, имеется ли тег (какое-то слово) в данном куске:  
https://gitlab.com/theyoungggod/news_classifier/-/blob/main/src/modules/slicer.py  

Использованные модули:  
```
from nltk.tokenize import sent_tokenize
from nltk.tokenize import word_tokenize
```
sent_tokenize - делит текст на предложения
word_tokenize - делит текст на слова

Разделение текста на абзацы
```
def split_into_paragr(text):
  return [paragr for paragr in text.split("\n") if len(paragr) > 0]
```
Проверка, есть ли тег (слово) в предложении
```
def check_tag(tags, sentence):
  arr_tags = word_tokenize(tags.lower())
  sentence_word_tokenized = word_tokenize(sentence.lower())
  for tag in arr_tags:
    if tag.lower() not in sentence_word_tokenized:
      return False
  return True
```
Функция возвращает определенное количество предложений в куске
```
def context_sentences(sentences, id, context_size):
  start_id = max(id - context_size, 0)
  end_id = id + context_size + 1
  return sentences[start_id:end_id]
```
Функция работает именно с абзацами, то есть для каждого абзаца проверяет, есть ли там тег с помощью check_tag(). При этом возвращает определенное число предложений (context_sentences())
```
def slicer_paragr(paragr, tag, context_size):
  paragr_with_tag = []
  sentences = sent_tokenize(paragr)
  for id, sentence in enumerate(sentences):
    if check_tag(tag, sentence):
      paragr_with_tag.append(' '.join(context_sentences(sentences, id, context_size)))
  return paragr_with_tag
  
```
"Главная" функция, от которой запускаются все другие. Делит статью на абзацы split_into_paragr() и для каждого абзаца выполняет slicer_paragr()
```
def slicer(text, tag, context_size):
  text_with_tag = []
  paragr_lst = split_into_paragr(text)
  for paragr in paragr_lst:
    text_with_tag.extend(slicer_paragr(paragr, tag, context_size))
  return text_with_tag
```
Просто скрипт, который использует стандартную библиотеку json  
https://gitlab.com/theyoungggod/news_classifier/-/blob/main/src/modules/data_to_json_file.py  
Запись в файл  
```
def data_to_json_file(data: json):
    with open('./data/data.json', 'a') as file:
        print(data)
        json.dump(data, file, ensure_ascii=False, indent=4)
```
Использование фреймворка FastAPI (здесь только использование логов писала не я):
https://gitlab.com/theyoungggod/news_classifier/-/blob/main/src/app.py  

дальше примеры, которые были написаны чисто для себя
### 2 пример 
http.server, pandas   
репозиторий:  
https://github.com/PavVlada/CitiesServer  
### 3 пример
django  
репозиторий:  
https://github.com/PavVlada/test  
### 4 пример  
Чуть больше FastAPI  
Репозиторий:
https://github.com/PavVlada/REST_API
