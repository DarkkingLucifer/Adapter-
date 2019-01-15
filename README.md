# Adapter-通用模板

```android
private XxAdapter adapter;

adapter = new XxAdapter(context, list);

 @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_special_time);
        ButterKnife.bind(this);
        initView();
        requestData();
    }

    private void initView() {
        employeeService = new EmployeeService(this);
        itemList = new ArrayList<>();

        shopId = mApplication.getCurrShopId() + "";
        adapter = new SpecialTimeAdapter(mActivity, itemList);
        rvSpecialTime.setLayoutManager(new LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false));
        rvSpecialTime.setAdapter(adapter);
    }

    private void requestData() {
        addDisposableIoMain(employeeService.listWeekRebateRate(shopId), new DefaultConsumer<List<WeekRebateRateBean>>(mApplication) {
            @Override
            public void operateSuccess(BaseResult<List<WeekRebateRateBean>> data) {
                itemList.clear();
                itemList.addAll(data.getData());
                adapter.notifyDataSetChanged();
            }
        });
    }

