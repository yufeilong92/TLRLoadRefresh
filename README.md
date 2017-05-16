# TLRLoadRefresh
TLRLoadRefresh��һ��֧��ListView,RecycleView,ViewGroup������ˢ�º��������ص�UI���,ʹ�þ��кܴ������ԡ����Ը����Լ��Ĳ�ͬ���������岻ͬUI��ƣ����������Զ�������ˢ�µ�Head���������ص�Foot�����潫���ܸÿؼ���ʹ�÷��������˼�룬�����ȿ���Ч����

![1](png/1.gif) ![2](png/2.gif) ![3](png/3.gif) ![4](png/4.gif)

# �ؼ����Խ���

����Կؼ����������½��ܣ���������в�����ĵط�����ҿ�����������demo�鿴��demo��Ҳ�õ����Լ�д��һ�������ܣ�[TCache](https://github.com/borneywpf/TCache)��Ҳ��ӭ���star��

## TLRLinearLayout���Խ���,���£�

```xml
    <declare-styleable name="TLRLinearLayout">
        <attr name="enableRefresh" format="boolean"/>
        <attr name="enableLoad" format="boolean"/>
        <attr name="refreshThreshold" format="float"/>
        <attr name="loadThreshold" format="float"/>
        <attr name="refreshMaxMoveDistance" format="dimension"/>
        <attr name="loadMaxMoveDistance" format="dimension"/>
        <attr name="closeAnimDuration" format="integer"/>
        <attr name="openAnimDuration" format="integer"/>
        <attr name="resistance" format="float"/>
        <attr name="releaseRefresh" format="boolean"/>
        <attr name="releaseLoad" format="boolean"/>
        <attr name="keepHeadRefreshing" format="boolean"/>
        <attr name="keepFootLoading" format="boolean"/>
        <attr name="keepContentLayout" format="boolean"/>
        <attr name="canMoveHeadByTLR" format="boolean"/>
        <attr name="canMoveFootByTLR" format="boolean"/>
    </declare-styleable>
```
- **enableRefresh** �Ƿ����ˢ��
- **enableLoad** �Ƿ���Լ���
- **refreshThreshold** ��ˢ��ϵ������Head View�ĸ߶�Ϊ������Ĭ����1.0f
- **loadThreshold** �ɼ���ϵ������Foot View�ĸ߶�Ϊ������Ĭ����1.0f
- **refreshMaxMoveDistance** ˢ��ʱ�������������߶ȣ��������Ҫ���ڼ���ϵ������ļ��ظ߶ȣ������޷�����ˢ��
- **loadMaxMoveDistance** ����ʱ�������������߶ȣ�ͬ��
- **closeAnimDuration** ˢ�½����Ķ���ʱ��
- **openAnimDuration** �Զ�ˢ�£���Head�Ķ���ʱ��
- **resistance** ������������ϵ����ϵ��Խ�󣬴���������Խ����
- **releaseRefresh** �Ƿ��ͷ�ˢ�£�Ĭ����
- **releaseLoad** �Ƿ��ͷż��أ�Ĭ����
- **keepHeadRefreshing** ˢ��ʱ���Ƿ񱣳�Head View
- **keepFootLoading** ����ʱ���Ƿ񱣳�Foot View
- **keepContentLayout** ���ػ�ˢ��ʱ���Ƿ񱣳������岿�ƶ�
- **canMoveHeadByTLR** ˢ��ʱ���Ƿ������Head Viewһ���ƶ�
- **canMoveFootByTLR** ����ʱ���Ƿ������Foot Viewһ���ƶ�

## TLRLinearLayout�ӿؼ�label����
```xml
    <declare-styleable name="TLRLinearLayout_Layout">
        <attr name="label" format="enum"> 
            <enum name="head" value="1"/><!--���view��ˢ�µ�head-->
            <enum name="content" value="2"/><!--���Ϊ��ˢ���壬TLRLinearLayout�����ж��ˢ���壬���Բ鿴demo-->
            <enum name="foot" value="3"/><!--���view�Ǽ��ص�foot-->
        </attr>
    </declare-styleable>
```

# TLRLinearLayout����TLRNestedLinearLayout

TLRNestedLinearLayout������֧��android��Ƕ�׻���������֧��RecycleView,NestedScrollView��Ƕ�׻���view������ˢ�º��������أ�������Բ鿴demo

# �ص��ӿ�TLRUIHandler����

```java
public interface TLRUIHandler {
    /**
     * ָ��viewˢ��״̬�Ļص�
     */
    void onRefreshStatusChanged(View target, TLRLinearLayout.RefreshStatus status);

    /**
     * ָ��view����״̬�Ļص�
     */
    void onLoadStatusChanged(View target, TLRLinearLayout.LoadStatus status);

    /**
     * ָ��view������Ϣ�Ļص�
     * @param target �ĸ�view������λ�ñ仯
     * @param isRefresh �Ƿ�ʱˢ��
     * @param totalOffsetY touch Y�����ƶ��ľ���
     * @param totalThresholdY Y����ͨ��ˢ��ϵ��������ƶ�����
     * @param offsetY Y��������ƶ��ľ���
     * @param threshOffset Y�����ƶ��仯ϵ��
     */
    void onOffsetChanged(View target, boolean isRefresh, int totalOffsetY, int totalThresholdY,
            int offsetY, float threshOffset);

    /**
     * ˢ�»�������ʱ״̬�Ļص�
     */
    void onFinish(View target, boolean isRefresh, boolean isSuccess, int errorCode);
}
```

# ˢ�»�������ʱhook keepview�ӿ�TLRUIHandlerHook

�ڼ��ػ�ˢ�����ʱ��head��foot view��ʱ�����һЩ�Լ��Ķ�������������ԭ����[MaterialHeaderView](https://github.com/borneywpf/TLRLoadRefresh/blob/master/library/src/main/java/com/think/tlr/MaterialHeaderView.java)�ڼ������ʱ��������һ����С������Ȼ������TLRLinearLayout���ʣ�µĶ�������ʱ����õ���TLRUIHandlerHook������ɲο�MaterialHeaderViewʵ�֡��������˼��Դ����[android-Ultra-Pull-To-Refresh](https://github.com/liaohuqiu/android-Ultra-Pull-To-Refresh),��л��ţ�ǵĹ��ס�

# ʵ��ԭ�����

����

# �ܽ�

��ʵ�ֹ������Ҳο���һЩ����Ŀ�Դ�⣬��л��Щ��˽�Ĵ�ţ�������Ĺ��ף������Ŀǰû�н�һ����װ����Ϊ�һ�û������ȫ��Ĳ��ԣ�������������⻶ӭ���ָ��������[issues](https://github.com/borneywpf/TLRLoadRefresh/issues)
  
