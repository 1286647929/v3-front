<script setup lang="ts">
import { LoginData } from '@/api/types'
// import ElFormRules from '../../presets/types/element'

const props = defineProps({
	visibale: Boolean,
})
const loginDialogVisible = computed(() => props.visibale)
const emits = defineEmits(['changeValue'])

const handleChange = () => {
	emits('changeValue', false)
}

const loginForm = ref<LoginData>({
	phone: '',
	code: '',
	rememberMe: false,
	uuid: '',
})

const loginRules: ElFormRules = {
	phone: [
		{
			required: true,
			trigger: 'blur',
			message: '请输入您的手机号',
		},
		{
			pattern: /^((0\d{2,3}-\d{7,8})|(1[34578]\d{9}))$/,
			trigger: 'blur',
			message: '手机号格式不正确',
		},
	],
	code: [
		{
			required: true,
			trigger: 'change',
			message: '请输入验证码',
		},
		{
			pattern: /^\d{4}$/,
			trigger: 'blur',
			message: '请输入4位数字验证码',
		},
	],
}

const loginRef = ref<ElFormInstance>()

/**
 * 登录
 */
const handleLogin = () => {
	loginRef.value?.validate(async (valid: boolean, fields: any) => {
		if (valid) {
			console.log(valid)
		} else {
			console.log('error submit!', fields)
		}
	})
}

/**
 * 表单重置
 */
const resetForm = () => {
	loginRef.value?.resetFields()
}
</script>

<template>
	<el-dialog
		:before-close="handleChange"
		:model-value="loginDialogVisible"
		width="500px"
		center
		@open="resetForm"
	>
		<template #header>
			<span class="text-3xl">登录</span>
		</template>
		<el-form
			ref="loginRef"
			:model="loginForm"
			:rules="loginRules"
			label-width="30px"
		>
			<el-form-item prop="phone">
				<div>
					<el-input
						v-model="loginForm.phone"
						placeholder="请输入手机号"
						maxlength="11"
						size="large"
						style="width: 380px; font-size: 24px; height: 50px"
					>
						<template #prefix>
							<span>+86</span>
						</template>
					</el-input>
				</div>
			</el-form-item>
			<el-form-item prop="code">
				<el-input
					v-model="loginForm.code"
					placeholder="请输入验证码"
					size="large"
					style="width: 380px; font-size: 24px; height: 50px"
				>
					<template #suffix>
						<el-button>获取验证码</el-button>
					</template>
				</el-input>
			</el-form-item>
			<el-form-item>
				<el-button
					type="primary"
					size="large"
					style="width: 380px; height: 50px; border-radius: 25px"
					@click="handleLogin"
				>
					登录
				</el-button>
			</el-form-item>
			<el-form-item prop="rememberMe">
				<el-checkbox v-model="loginForm.rememberMe" label="下次自动登录" />
			</el-form-item>
		</el-form>
		<template #footer>
			<div class="dialog-footer">
				<span>微信登录</span>
				<div>
					<el-image
						style="cursor: pointer; margin-top: 10px"
						src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAAAXNSR0IArs4c6QAABUBJREFUaEPVmmfIXFUQhp/XAvYWEYVoVGyICsGSIKhYfigaxYJG0BiNIcaCJQkoggWVoMYYjWIkCkYFoxKwRAMKRtEfRrFgAY3+ELFjjRUsI+/m7Mfd69177u5++LEDy8Kec+bMe8+cmXfmrhgFiYgdgCOBycDewJ6Af9ssqf8N+Ab4CPgQeBVYLcm/DSTqd3VEbAecCZwNHAL0qiuA14CHgEckfd+PLb1uSkTsBMwFZgGb97NpxZpfgXuBBZK+7EVnYwARsTFwKXAtsEUvm/Qw9xfgeuAOSX82WdcIQETsATwGTGyidBTmvAWcLunjnK4sgIg4CXgQ2CqnbJTH1wHTJD1Zp7cWQETMBO4BNhxl45qq+xuYLWlptwVdASTjfbGyp9TUmj7nOVrN6gai0rjkNivG8MmXsfokTq1yp/8ASBf2jTHw+dwB+U4cWL7YHQBSqFzzP0abnNHlcUenScUQWwbgBHVrD1o/BZ4H3gY+A35P9GHn9BCOAcb3oK/J1HmSFrQnjgBIGXZtwyT1HDBf0ot1O0aE9R8FXJ24UhMDc3Oc7PZqZ+wigNuAKzKrfwBmSvIF70ki4rQUkrfvaWH15IWS5nioBSARM7tDHbf5Ajha0gf9GhARuyeX8/cgYu60iwlgG8BFwF01Gv8ADpXkSzQidhFJjtOVEhEbSPqntMa05HVgm0EQABdLursNwPx8Uo3CayTdUDLkEuBmwHzF4OybRXD3AeckqjytNDYD8PggskbSZKVi5KuajOv4O17SzyUjzOUPTr8dIOnd9rifPOBj3gT4TlKH30eEqYkDxiCu5JPf0QDOAJbXPIrlkly4dEhE7J/qgrWSbqoYPwE4C1gh6fECuE1TpJsH+DOITDWA24HLarTMleQI1bdExBHAdGA34OuUM8z3fTL7OcMCG/WxwSIDeBY4rmbxdEnL+lDu6DYBWJIMXizpnSo9EWEg56YTdS3dVFYZgAttR4Zu0rrtTTUWXMX3YzFwoaQ3m6yPCEcm0/epTeY7gBjATxnitkTS7IYKW9MiYlfgYeCUfjoPEbEQuLzBnusMwL5Y53+fAxMkmdI2koh4Ariy36SXKMgzGde2LX81AeCJ50u6v4n1EeHekLl7R4SJCJ/IFLdiJPnetU/rxvS07Wojdy1lbfeQ6h5uC0DOhbyRezYTJZlu1EpELLIfS/LmIxIRLwCHAzNKhjqhnQdcJcmJsbjmacDhuJu0XCh3iduL30tcqLabFhFPSTqxvGNE+EluKcmEsGik2cA4Sd9WrPEp3lIDoHWJc2G0uN5gT5b0fjel3QDkTq5qPCJMRR6oWdsKo7lEVl6/TJKTUqVExCpJdXmlMZaIyBVYrUSWoxLlDadIWhkRWyey9ol7nJLMpxxCHwXmSHKFNpBExErg+BolLSrhzFdH5orrf0yd5wtS8bNtYdDlpD9uO14naf4g1kfEPoAJYrcotJ7MpaeWo9NtWwzUPdJxGeMctfaVZN7TsyS2uho4rGbxejqdAOQKmp6NAF4CjpXkYqixJCruTpxDa510FDTu9edKysZGFCa+nJq0rfuRk4jwCxEnM9fPddJZUqZTaFLU52yoGrc7+T4sleSk2VUiwq5pt8v1YjuL+gTALy6atlX6AeIL7jaM62HzK3Mr948OAnxh70xM9JX0xqfbHtVtlQQiF3f7MbyXNaYfPgFTjm5S3dhKABxhhre1mEC4uBnO5m77zIa6vV4A4bczw/mCowRiOF8xldxpOF/yFUAM72vWAojhfdFdzChD+1eDcloc2j97VOX3sfy7zb+KQyYXaTIqRQAAAABJRU5ErkJggg=="
					></el-image>
				</div>
				<div style="margin-top: 10px">
					<span>未注册手机验证后自动登录，登录或注册即代表同意</span>
					<a href="#" style="color: #d96922">用户协议</a>
					<span>和</span>
					<a href="#" style="color: #d96922">隐私政策</a>
				</div>
			</div>
		</template>
	</el-dialog>
</template>

<style scoped lang="scss">
:deep(.el-input__wrapper) {
	border-radius: 25px;
}
</style>
