# Các phương thức suggest trong Optuna

Optuna cung cấp một số phương thức để gợi ý các giá trị cho các siêu tham số trong quá trình tối ưu hóa.

## 1. suggest_int

Phương thức này gợi ý một giá trị nguyên ngẫu nhiên trong phạm vi được chỉ định.

**Cú pháp**: `trial.suggest_int(name, low, high, step=1)`

**Tham số**:

- `name`: Tên của siêu tham số.
- `low`: Giá trị nhỏ nhất của phạm vi.
- `high`: Giá trị lớn nhất của phạm vi.
- `step`: Bước nhảy giữa các giá trị nguyên (mặc định là 1).

Ví dụ:
```Python
trial.suggest_int("num_layers", 1, 5)
```

## 2. suggest_categorical

Phương thức này gợi ý một giá trị ngẫu nhiên từ một danh sách các lựa chọn.

Cú pháp: `trial.suggest_categorical(name, choices)`

**Tham số**:

- `name`: Tên của siêu tham số.
- `choices`: Danh sách các lựa chọn cho siêu tham số.

**Ví dụ**:

```Python
trial.suggest_categorical("activation", ["relu", "tanh", "sigmoid"])
```

## 3. suggest_uniform

Phương thức này gợi ý một giá trị thực ngẫu nhiên trong phạm vi được chỉ định với phân phối đều.

**Cú pháp**: `trial.suggest_uniform(name, low, high)`

**Tham số**:

- `name`: Tên của siêu tham số.
- `low`: Giá trị nhỏ nhất của phạm vi.
- `high`: Giá trị lớn nhất của phạm vi.

**Ví dụ**:

```Python
trial.suggest_uniform("learning_rate", 0.001, 0.1)
```

## 4. suggest_loguniform

Phương thức này gợi ý một giá trị thực ngẫu nhiên trong phạm vi được chỉ định với phân phối logarit đều.

**Cú pháp**: `trial.suggest_loguniform(name, low, high)`

**Tham số**:

- `name`: Tên của siêu tham số.
- `low`: Giá trị nhỏ nhất của phạm vi (trên thang logarit).
- `high`: Giá trị lớn nhất của phạm vi (trên thang logarit).

```Python
trial.suggest_loguniform("dropout_rate", 0.001, 0.1)
```
## Lựa chọn phương thức suggest phù hợp:

Lựa chọn phương thức suggest phù hợp phụ thuộc vào loại dữ liệu và phân phối mong muốn của siêu tham số:

- **suggest_int**: Sử dụng cho các siêu tham số là giá trị nguyên.
- **suggest_categorical**: Sử dụng cho các siêu tham số có một số lượng lựa chọn hữu hạn.
- **suggest_uniform**: Sử dụng cho các siêu tham số là giá trị thực với phân phối đều.
- **suggest_loguniform**: Sử dụng cho các siêu tham số là giá trị thực với phân phối logarit đều.
## Lưu ý:

- Các phương thức suggest chỉ gợi ý các giá trị cho siêu tham số. Việc lựa chọn giá trị thực tế được sử dụng trong quá trình huấn luyện mô hình sẽ phụ thuộc vào thuật toán tối ưu hóa được sử dụng.
- Có thể sử dụng nhiều phương thức suggest trong cùng một thử nghiệm.
## Ví dụ

Dưới đây là ví dụ minh họa cách sử dụng các phương thức suggest:

```Python
from optuna import create_study, Trial

def objective(trial):
    num_layers = trial.suggest_int("num_layers", 1, 5)
    activation = trial.suggest_categorical("activation", ["relu", "tanh", "sigmoid"])
    learning_rate = trial.suggest_uniform("learning_rate", 0.001, 0.1)
    dropout_rate = trial.suggest_loguniform("dropout_rate", 0.001, 0.1)

    # Huấn luyện mô hình với các giá trị siêu tham số được gợi ý

    return score

study = create_study()
study.optimize(objective, n_trials=100)

best_params = study.best_params

print(best_params)
```