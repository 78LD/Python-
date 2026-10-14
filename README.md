from itertools import permutations
from pathlib import Path


def generate_possibilities():
    print("=" * 40)
    print("     مولّد الاحتمالات باستخدام Python")
    print("=" * 40)

    print("أدخل كل معلومة في سطر جديد.")
    print("اترك سطرًا فارغًا عند الانتهاء:")

    items = []

    while True:
        item = input().strip()

        if not item:
            break

        items.append(item)

    if not items:
        print("لم تدخل أي معلومات!")
        return

    try:
        max_length = int(
            input("أدخل الحد الأقصى لطول الاحتمالات: ")
        )
    except ValueError:
        print("يرجى إدخال رقم صحيح.")
        return

    if max_length < 1:
        print("يجب أن يكون الحد الأقصى 1 أو أكثر.")
        return

    max_length = min(max_length, len(items))

    output_file = Path("possibilities.txt")
    count = 0

    with output_file.open("w", encoding="utf-8") as file:
        for length in range(1, max_length + 1):
            for possibility in permutations(items, length):
                result = "".join(possibility)
                file.write(result + "\n")
                count += 1

    print(f"\nتم إنشاء {count} احتمالًا.")
    print(f"تم حفظ النتائج في: {output_file.resolve()}")


if __name__ == "__main__":
    generate_possibilities()
