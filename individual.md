                Індивідуальна робота     

Автор:Коломійченко Богдан Сергійович
Група:ІПЗ-13
Варіант:8

                           Завдання

8. Генератор паролів, логінів, ніків, афоризмів тощо

import random
def gener(n):
    ru_word_sm = ['а', 'б','в','г','д', 'е','ё','ж','з','и','й', 'к','л', 'м','н','о','п','р','с',
                  'т','у','ф','х','ц','ч','ш','щ','ъ','ы','ь','э','ю','я']  #1
    ru_word_bg = ['А','Б','В','Г','Д','Е','Ё','Ж','З','И','Й','К','Л','М','Н','О','П','Р','С',
                  'Т','У','Ф','Х','Ц','Ч','Ш','Щ','Ъ','Ы','Ь','Э','Ю','Я'] #2
    eng_word_sm = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t',
                   'u','v','w','x','y','z'] #3
    eng_word_bg = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q',
                   'R','S','T','U','V','W','X','Y','Z'] #4
    numb = ['1','2','3','4','5','6','7','8','9','0']  # Нуля немає, щоб не плутатись з буквою О  #5

    spec_sym = ['!','@','#','$','%','^','&','*','(',')','_','+',';',';','?','-','`','/','<','>',
                '[',']','{','}']  #6
#=======Російські маленькі з іншими(=============
    ru_sm_bg = ru_word_sm + ru_word_bg  #7
    ru_sm_eng_sm = ru_word_sm + eng_word_sm #8
    ru_sm_eng_bg = ru_word_sm + eng_word_bg #9
    ru_sm_numb = ru_word_sm + numb #10
    ru_sm_spec = ru_word_sm + spec_sym #11
#=========Російські великі з іншими==========
    ru_bg_eng_sm = ru_word_bg + eng_word_sm #12
    ru_bg_eng_bg = ru_word_bg + eng_word_bg #13
    ru_bg_numb = ru_word_bg + numb #14
    ru_bg_spec = ru_word_bg + spec_sym  #15
#=========Англійські маленькі з іншими=========
    eng_sm_bg = eng_word_sm + eng_word_bg #16
    eng_sm_numb = eng_word_sm + numb #17
    eng_sm_spec = eng_word_sm + spec_sym #18
#========Англійські великі з іншими===========
    eng_bg_numb = eng_word_bg + numb #19
    eng_bg_spec = eng_word_bg + spec_sym #20
#========Числа з іншими ============
    numb_spec = numb + spec_sym    #21

#=======Російські маленькі + рос. великі з іншими========
    ru_sm_bg_eng_sm = ru_sm_bg + eng_word_sm #22
    ru_sm_bg_eng_bg = ru_sm_bg + eng_word_bg #23
    ru_sm_bg_numb = ru_sm_bg + numb #24
    ru_sm_bg_spec = ru_sm_bg + spec_sym #25
#========Англійські маленькі + англ. великі з іншими==========
    eng_sm_bg_numb = eng_sm_bg + numb #26
    eng_sm_bg_spec = eng_sm_bg + spec_sym #27
#========Всі можливі набори============
    all_r = ru_sm_bg + eng_sm_bg + numb + spec_sym





    #print(numb + spec_sym)
    if n == 1:
        return ru_word_sm
    elif n == 2:
        return ru_word_bg
    elif n == 3:
        return eng_word_sm
    elif n == 4:
        return eng_word_bg
    elif n == 5:
        return numb
    elif n == 6:
        return spec_sym
    elif n == 7:
        return ru_sm_bg
    elif n == 8:
        return ru_sm_eng_sm
    elif n == 9:
        return ru_sm_eng_bg
    elif n == 10:
        return ru_sm_numb
    elif n == 11:
        return ru_sm_spec
    elif n == 12:
        return ru_bg_eng_sm
    elif n == 13:
        return ru_bg_eng_bg
    elif n == 14:
        return ru_bg_numb
    elif n == 15:
        return ru_bg_spec
    elif n == 16:
        return eng_sm_bg
    elif n == 17:
        return eng_sm_numb
    elif n == 18:
        return eng_sm_spec
    elif n == 19:
        return eng_bg_numb
    elif n == 20:
        return eng_bg_spec
    elif n == 21:
        return numb_spec
    elif n == 22:
        return ru_sm_bg_eng_sm
    elif n == 23:
        return ru_sm_bg_eng_bg
    elif n == 24:
        return ru_sm_bg_numb
    elif n == 25:
        return ru_sm_bg_spec
    elif n == 26:
        return eng_sm_bg_numb
    elif n == 27:
        return eng_sm_bg_spec
    elif n == 28:
        return all_r

def gene_de ():
    print('Виберіть один з можливих варіантів: ')
    print('1 - Рос. мал.')
    print('2 - Рос. вел.')
    print('3 - Англ. мал.')
    print('4 - Англ. вел.')
    print('5 - Числа')
    print('6 - Спец. символи')
    print('7 - Рос. мал. + вел.')
    print('8 - Рос. мал. + англ. мал.')
    print('9 - Рос. мал. + англ. вел.')
    print('10 - Рос. мал. + числа')
    print('11 - Рос. мал. + спец. символи')
    print('12 - Рос. вел. + англ. мал.')
    print('13 - Рос. вел. + англ. вел.')
    print('14 - Рос. вел. + числа')
    print('15 - Рос. вел. + спец. символи')
    print('16 - Англ. мал. + англ. вел.')
    print('17 - Англ. мал. + числа')
    print('18 - Англ. мал + спец. символи')
    print('19 - Англ. вел. + числа')
    print('20 - Англ. вел. + спец. символи')
    print('21 - Числа + спец. символи')
    print('22 - Рос. мал. + рос. вел. + англ. мал.')
    print('23 - Рос. мал + рос. вел. + англ. вел.')
    print('24 - Рос. мал. + рос. вел. + числа')
    print('25 - Рос. мал. + рос. вел. + спец.символи')
    print('26 - Англ. мал. + англ. вел. + числа')
    print('27 - Англ. мал. + англ. вел. + спец. символи')
    print('28 - Всі можливі набори')

    n = int(input('Виберіть спосіб: '))
    k = int(input('Виберіть довжину пароля/ніку: '))
    nabor = gener(n)
    lst = []
    for i in range(k):
        ran = random.randint(0, len(nabor)-1)
        lst += nabor[ran]
        global result
        result = ''.join(lst)

    print('Ваш пароль/нік: ', result)

gene_de()








