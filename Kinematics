from math import *
from operator import *

def kinematics():
    variables = {'d': 0, 't': 0, 'a': 0, 'vi' : 0, 'vf': 0}
    print ("Variable must be 'd', 't', 'a', 'vi', or 'vf' ")
    print ("")
    print ("Assume these variables have the proper units for conversion.")
    question = input('Variable?: ')
    assert question in variables, "Variable must be 'd', 't', 'a', 'vi', or 'vf' "
    print ("")
    print("If no variable is given, please write N/A ")
    print ("")

    errorswitcher = False

    for key in variables.keys():
        if key == question:
            variables[key] = 'N/A'
        else:
            ask = input('What is the value of ' + key + ': ')
            print("")
            variables[key] = ask

            if variables[key] == 'N/A':
                if errorswitcher:
                    assert False, "Child, you can't have more than 2 unknowns."
                errorswitcher = True

            elif type(float(ask)) is float:
                variables[key] = float(ask)

            elif type(int(ask)) is int:
                variables[key] = int(ask)

            elif type(variables[key]) not in (int, float):
                assert False, "Child, you don't know physics."

            else:
                assert False, "Child, you are trying to do something beyond my capabilities."

    print('Now calculating value for ' + question)

    #Calculator will compute the question will take in two arguments, the question and the dictionary of variables.

    def calculator(question, variables):
        if question == 'd':
            if variables['vi'] != 'N/A' and variables['a'] != 'N/A' and variables['t'] != 'N/A':
                variables[question] = add(variables['vi'] * variables['t'], 0.5 * variables['a'] * variables['t'] * variables['t'])

            elif variables['vi'] != 'N/A' and variables['vf'] != 'N/A' and variables['t'] != 'N/A':
                variables[question] = mul(variables['vi'] + variables['vf'], 0.5 * variables['t'])

            elif variables['vi'] == 'N/A':
                variables['vi'] = sub(variables['vf'], variables['a'] * variables['t'])
                return calculator(question, variables)

            elif variables['t'] == 'N/A':
                try:
                    variables['t'] = sub(variables['vf'], variables['vi']) / variables['a']
                except ZeroDivisionError:
                     return print('Acceleration was zero...', "lol it's not constant velocity without time!! ", 'Child, know your physics!')

                return calculator(question, variables)


        elif question == 'vf':
            if variables['vi'] != 'N/A' and variables['a'] != 'N/A' and variables['d'] != 'N/A':
                variables[question] = sqrt(mul(variables['vi'], variables['vi']) + mul(2 * variables['a'], variables['d']))

            elif variables['vi'] != 'N/A' and variables['a'] != 'N/A' and variables['t'] != 'N/A':
                variables[question] = add(variables['vi'], variables['a'] * variables['t'])

            elif variables['vi'] == 'N/A':
                try:
                    variables['vi'] = sub(variables['d'], 0.5 * variables['a'] * variables['t'] * variables['t']) / variables['t']
                except ZeroDivisionError:
                    return print("So if time was 0... Can you even move? Are you god?")

                return calculator(question, variables)

            elif variables['a'] == 'N/A':
                try:
                    variables['a'] = mul(2, sub(variables['d'], variables['vi'] * variables['t'])) / mul(variables['t'], variables['t'])
                except ZeroDivisionError:
                    return print("So if time was 0... Can you even move? Are you god?")

                return calculator(question, variables)


        elif question == 'vi':
            if variables['vf'] != 'N/A' and variables['a'] != 'N/A' and variables ['t'] != 'N/A':
                variables[question] = sub(variables['vf'], variables['a'] * variables['t'])

            elif variables['d'] != 'N/A' and variables['t'] != 'N/A' and variables ['vf'] != 'N/A':
                try:
                    variables[question] = sub(mul(2, variables['d']) / variables['t'], variables['vf'])
                except ZeroDivisionError:
                    return print("You can't freeze time man.")

            elif variables['vf'] == 'N/A':
                variables[question] = sub(variables['d'], 0.5 * variables['a'] * variables['t'] * variables['t']) / variables['t']

            elif variables['t'] == 'N/A':
                variables[question] = sqrt(sub(mul(variables['vf'], variables['vf']), 2 * variables['a'] * variables['d']))


        elif question == 'a':
            if variables['vf'] != 'N/A' and variables['vi'] != 'N/A' and variables['t'] != 'N/A':
                try:
                    variables[question] = sub(variables['vf'], variables['vi']) / variables['t']
                except ZeroDivisionError:
                    return print("Child. Repeat my course next year. You don't know what time is.")

            elif variables['vf'] != 'N/A' and variables['vi'] != 'N/A' and variables['d'] != 'N/A':
                try:
                    variables[question] = sub(variables['vf'] * variables['vf'], variables['vi'] * variables['vi']) / mul(2, variables['d'])
                except ZeroDivisionError:
                    return print("You assign a block to not move. Can it have velocity?")

            elif variables['d'] != 'N/A' and variables['vi'] != 'N/A' and variables['t'] != 'N/A':
                try:
                    variables['a'] = mul(2, sub(variables['d'], variables['vi'] * variables['t'])) / mul(variables['t'], variables['t'])
                except ZeroDivisionError:
                    return print("So if time was 0... Can you even move? Are you god?")

            elif variables['vi'] == 'N/A':
                try:
                    variables['vi'] = sub(mul(2, variables['d']) / variables['t'], variables['vf'])
                except ZeroDivisionError:
                    return print("You can't freeze time man.")

                return calculator(question, variables)


        elif question == 't':
            if variables['vf'] != 'N/A' and variables['vi'] != 'N/A' and variables['a'] != 'N/A':
                try:
                    variables[question] = sub(variables['vf'], variables['vi']) / variables['a']
                except ZeroDivisionError:
                    return print('Acceleration was zero...', "lol it's not constant velocity without time!! ", 'Child, know your physics!')

            elif variables['d'] != 'N/A' and variables['vi'] != 'N/A' and variables['vf'] != 'N/A':
                try:
                    variables[question] = mul(2, variables['d']) / add(variables['vi'], variables['vf'])
                except ZeroDivisionError:
                    return print("Child... your system doesn't make any sense! Go take AP Physics C: Mechanics.")

            elif variables['a'] != 'N/A' and variables['vi'] != 'N/A' and variables['d'] != 'N/A': #Quadratic equation
                discriminant = add(mul(variables['vi'], variables['vi']), mul(2 * variables['a'], variables['d']))    # discriminant

                if discriminant < 0:
                    return print ("Child... What on earth is your time??")

                elif discriminant == 0:
                    variables[question] = -variables['vi']  / (2 * variables['a'])
                else:
                    x1 = (-variables['vi'] + sqrt(discriminant)) / (variables['a'])
                    x2 = (-variables['vi'] - sqrt(discriminant)) / (variables['a'])
                    print ("This equation has two solutions: ", x1, " or", x2)
                    print ("However, time is only positive...")
                    return print ("So the answer is", max(x1, x2))

            elif variables['vi'] == 'N/A':
                variables['vi'] = sqrt(sub(mul(variables['vf'], variables['vf']), 2 * variables['a'] * variables['d']))
                return calculator(question, variables)


        print (variables[question])
        print ("")
        print ("")
        return print("Enter new variable for next problem!")

    return calculator(question, variables)

def recursion():
    kinematics()
    recursion()

recursion()



