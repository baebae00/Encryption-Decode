# Encryption-Decode
### Encrypt/decode file contents using .txt file

```python
import random
import os

origin = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'


def enc(data, enckey):
    result = ''
    for c in data:
        if(c in origin):
            result += enckey[origin.index(c)]
        else:
            result += c
    return result


def dec(data, enckey):
    result = ''
    for c in data:
        if(c in origin):
            result += origin[enckey.index(c)]
        else:
            result += c
    return result


def make():
    f = open('code.txt', 'a',encoding='utf-8')
    f.close()

    f = open('code.txt', 'r',encoding='utf-8')
    data = f.readlines()
    code = {}
    for line in data:
        file, encdata = line.strip().split()
        code[file] = encdata
    return code

def save(code):
    f = open('code.txt', 'w',encoding='utf-8')
    for key in code.keys():
        f.write(key+' '+code[key]+'\n')
    f.close()


def hard(file):
    entries = os.listdir('./')
    if(file in entries):
        return True
    else:
        return False

def createCodebook():
    code = make()
    file = input('파일 이름을 입력받겠습니다.: ')

    if file in code.keys():   
        if(hard(file)):
            data_file = open(file, 'r',encoding='utf-8')
            encdata = data_file.read()
            data_file.close()
            decdata = dec(encdata, code[file])
            data_file = open(file, 'w',encoding='utf-8')
            data_file.write(decdata)
            data_file.close()
            code.pop(file)
            save(code)
        else:
            print(file, '라는 파일은 없습니다.')
    else:                        
        if(hard(file)):
            enctext = list('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789')
            random.shuffle(enctext)
            data_file = open(file, 'r',encoding='utf-8')
            data = data_file.read()
            data_file.close()
            encdata = enc(data, enctext)
            data_file = open(file, 'w',encoding='utf-8')
            data_file.write(encdata)
            data_file.close()
            code[file] = ''.join(enctext)
            save(code)
        else:
            print(file, '라는 파일은 없습니다.')
    

createCodebook()

```
