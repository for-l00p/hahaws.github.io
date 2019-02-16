## 使用Airflow中遇到的小问题
- 动态创建Task
- 在Task之间传递参数
#### 动态创建Task
`有时候Task的数量不是一开始就是固定的,而是在Python程序运行中根据实际情况变动的, 那么动态创建Task就是必须的手段了` 
```
def manager():
    return ['1','2','3','4']

def print_n(n):
    print(n)

m=PythonOperator(
    task_id='manager'
    python_callable=manager
    dag=dag
)

def generate(i):
    t=PythonOperator(
        task_id='task_'+i
        python_callable=print
        dag=dag
    )

for i in manager():
    m >> generate(i)
```

