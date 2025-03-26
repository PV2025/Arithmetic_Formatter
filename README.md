# Arithmetic_Formatter

def arithmetic_arranger(problems, show_answers=False):
    # Error check 1: Too many problems
    if len(problems) > 5:
        return 'Error: Too many problems.'

    first_line = []
    second_line = []
    dash_line = []
    answers_line = []

    for problem in problems:
        parts = problem.split()

        if len(parts) != 3:
            return "Error: Invalid problem format."

        left, operator, right = parts

        # Error check 2: Invalid operator
        if operator not in ['+', '-']:
            return "Error: Operator must be '+' or '-'."

        # Error check 3: Non-digit characters
        if not left.isdigit() or not right.isdigit():
            return 'Error: Numbers must only contain digits.'

        # Error check 4: More than four digits
        if len(left) > 4 or len(right) > 4:
            return 'Error: Numbers cannot be more than four digits.'

        # Determine the width needed for alignment
        width = max(len(left), len(right)) + 2

        # Build each line
        first_line.append(left.rjust(width))
        second_line.append(operator + right.rjust(width - 1))
        dash_line.append('-' * width)

        if show_answers:
            result = str(eval(left + operator + right))
            answers_line.append(result.rjust(width))

    # Assemble all parts with 4 spaces between
    arranged = '    '.join(first_line) + '\n' + \
               '    '.join(second_line) + '\n' + \
               '    '.join(dash_line)

    if show_answers:
        arranged += '\n' + '    '.join(answers_line)

    return arranged
