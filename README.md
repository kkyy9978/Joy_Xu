# Joy_Xu
technical assessment 

# Q1
n = int(input())
t_shirts = input().split()
m = int(input())
requests = input().split()


t_shirts_count = {}
for size in t_shirts:
    if size in t_shirts_count:
        t_shirts_count[size] += 1
    else:
        t_shirts_count[size] = 1


for size in requests:
    found = False
    for key in t_shirts_count:
        if key.endswith(size) and t_shirts_count[key] > 0:
            found = True
            t_shirts_count[key] -= 1
            break
    if not found:
        print("No")
        break
else:
    print("Yes")

# Q2
n = int(input())
records = []
for i in range(n):
    record = input().split()
    records.append({
        "id": record[0],
        "isValid": record[1] == "true",
        "errorMessage": record[2] if len(record) > 2 else ""
    })

allValid = True
errorCodes = []
for record in records:
    if not record["isValid"]:
        allValid = False
        errorCodes.append(record["errorMessage"])

if allValid:
    print("Yes")
else:
    print("No")
    print(" ".join(errorCodes))


# Q3
SELECT o.owner_id, o.owner_name, COUNT(DISTINCT c.category_name) AS different_category_count
FROM articles a
JOIN categories c ON a.category_id = c.category_id
JOIN owners o ON a.owner_id = o.owner_id
GROUP BY o.owner_id, o.owner_name
ORDER BY different_category_count DESC
