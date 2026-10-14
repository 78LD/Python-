from itertools import permutations, product
from pathlib import Path
def generate_possibilities():
    print("=" * 45)
    print("      ALL POSSIBILITIES GENERATOR")
    print("          Repetition: 1 to 3")
    print("               Example: 78LD")
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
    items = list(dict.fromkeys(items))
    if not items:
        print("Error: No information entered.")
        return
    output_file = Path("possibilities.txt")
    seen = set()
    count = 0
    with output_file.open("w", encoding="utf-8") as file:
        # Generate combinations of 1, 2, and 3 entries
        for length in range(1, len(items) * 3 + 1):
            for combination in product(items, repeat=length):
                # No entry can occur more than 3 times
                valid = all(
                    combination.count(item) <= 3
                    for item in set(combination)
                )
                if not valid:
                    continue
                result = "".join(combination)
                if result not in seen:
                    seen.add(result)
                    file.write(result + "\n")
                    count += 1
    print("\nGeneration completed successfully!")
    print(f"Total unique possibilities: {count}")
    print(f"Saved to: {output_file.resolve()}")
if __name__ == "__main__":
    generate_possibilities()
