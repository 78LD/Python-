from itertools import permutations
from pathlib import Path
def generate_possibilities():
    print("=" * 45)
    print("       ALL POSSIBILITIES GENERATOR")
    print("              Example: 78LD")
    print("=" * 45)
    print("\nEnter your information, one item per line.")
    print("Press Enter on an empty line when finished.\n")
    items = []
    while True:
        item = input("> ").strip()
        if not item:
            break
        items.append(item)
    if not items:
        print("\nError: No information entered.")
        return
    # Generate every unique ordering
    unique_items = list(dict.fromkeys(items))
    possibilities = set(permutations(unique_items))
    output_file = Path("possibilities.txt")
    count = 0
    with output_file.open("w", encoding="utf-8") as file:
        for possibility in sorted(possibilities):
            result = "".join(possibility)
            file.write(result + "\n")
            count += 1
    print("\nGeneration completed successfully!")
    print(f"Total possibilities: {count}")
    print(f"Saved to: {output_file.resolve()}")
if __name__ == "__main__":
    generate_possibilities()
