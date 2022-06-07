# converter_base10to2or8
from typing import Union

def type_change(num: Union[int,float])->None:
    if (num.isdecimal() == False):
        try:
            return float(num)
        except ValueError as v:
            print(f"ValueError:整数か浮動小数点を入力してください")
    else:
        return int(num)


def convert_base(num: Union[int,float],base:int) -> Union[int,float]:
    t = "int"if type(num) == type(int()) else "float"
    if (t == "int"):
        result = ""
        if((base == 2 or base == 8)):
            while(num//base != 0):
                result += f"{num%base}"
                num = num//base
            result += f"{num%base}"
            return result[::-1]
    elif(t == "float"):
        i_result = ""
        d_result = ""
        i = int(num)
        d = (num - int(num))
        cnt = 9
        if((base == 2) or (base == 8)):
            while(i//base != 0):
                i_result += f"{i%base}"
                i = i//base
            i_result += f"{i%base}"
            i_result = i_result[::-1]
            i_result+= "."
            while(d%base != 0 and cnt > 0):
                d *= base
                d_result += f"{int(d)}"
                d -= int(d)
                cnt -= 1
            return i_result + d_result
    else:
        print("SelectionError:基数は2または8に限られます")

num = input("Enter the decimal number you want to convert:")
base = int(input("Enter the base you want to convert to (b):"))

num = type_change(num)

result = convert_base(num,base)
print(f"The base-{base} equivalent of {num} is {result}")
