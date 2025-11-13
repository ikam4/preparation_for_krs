Рюкзаки:
Обычный рюкзак (сложность O(n*m))
```cpp
    //dp[w] — можно ли набрать вес w
    vector<bool> dp(W + 1, false);
    dp[0] = true;

    // Для восстановления ответа
    vector used(n, vector<bool>(W + 1, false));

    for (int i = 0; i < n; ++i) {
        for (int w = W; w >= weights[i]; --w) {
            if (dp[w - weights[i]] && !dp[w]) {
                dp[w] = true;
                used[i][w] = true;
            }
        }
    }

    // Находим максимальный вес, который можно набрать
    int maxW = W;
    while (maxW >= 0 && !dp[maxW]) --maxW;

    cout << "Максимальный вес: " << maxW << endl;

    // Восстановление ответа
    vector<int> ans;
    int currentW = maxW;
    for (int i = n - 1; i >= 0; --i) {
        if (used[i][currentW]) {
            ans.push_back(i);
            currentW -= weights[i];
        }
  }```
