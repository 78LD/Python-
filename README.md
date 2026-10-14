from itertools import permutations
from pathlib import Path
def generate_possibilities():
    print("=" * 45)
    print("    ALL POSSIBILITIES GENERATOR")
    print("             Example: 78LD")
    print("=" * 45)
    print("\nEnter each word or phrase on a separate line.")
    print("Each entry will remain complete.")
    print("Press Enter on an empty line to finish.\n")
    items = []
    while True:
        item = input("> ").strip()
        if not item:
            break
        items.append(item)
    if not items:
        print("Error: No information entered.")
        return
    # Remove duplicate entries while preserving their original order
    items = list(dict.fromkeys(items))
    total = 1
    for number in range(1, len(items) + 1):
        total *= number
    output_file = Path("possibilities.txt")
    with output_file.open("w", encoding="utf-8") as file:
        for combination in permutations(items):
            file.write("".join(combination) + "\n")
    print("\nGeneration completed!")
    print(f"Total possibilities: {total}")
    print(f"Saved to: {output_file.resolve()}")
if __name__ == "__main__":
    generate_possibilities()
