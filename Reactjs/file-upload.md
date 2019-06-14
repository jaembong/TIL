# 파일 업로드

## 사용 환경

1. 서버 : nodejs, express, multer
2. 클라이언트 : reactjs, redux, immutable, redux-form, axios,

## 개요

1. file input 의 onChange -> 액션 -> 리듀서 -> 파일 객체 스토어에 저장
2. submit -> handleSubmit -> 스토어에서 폼 데이터와 파일 데이터를 axios를 통해 보냄.

## Example

Action

```javascript
export const files = (files, fieldName) => ({
    type: 'ACTION_FILES',
    files,
    fieldName
});
```

Reducer

```javascript
import { fromJS } from 'immutable';
initialState = fromJS({
    files: {},
});

export default (state = initialState, action) => {
    switch(action.type) {
        case 'ACTION_FILES':
            return state.setIn(['files', action.fieldName], action.files);
        default:
            return state;
    }
}
```

Component

```JSX
import React from 'react';
import { connect } from 'react-redux';
import { reduxForm, Field } from 'redux-from/immutable';

const FileTest = props => {
    const {
        filesData,
        formData,
        onFiles,
    } = props;

    const postForm = async (data) => {
        let config = {
            headers: {
                'Content-Type': 'multipart/form-data',
            }
        }
        return axios.post(
            `http://localhost:3001/files`,
            data,
            config
        ).then((response) => {
            return response;
        }).catch((err) => {
            throw err;
        });
    }

    const handleFiles = (e) => {
        onFiles(e.target.files[0], e.target.name);
    }

    const onFormSubmit = async (e) => {
        e.preventDefault();
        let form = formData.values;
        let sendData = new FormData();
        Object.keys(formD).map((v) => {
            sendData.append(v, form[v]);
        });
        let files = filesData.toJS();
        Object.keys(files).map((v) => {
            sendData.append(v, files[v]);
        });
        try {
            let result = await postForm(sendData);
        }
        catch (err) {
            console.log(err);
        }
    }

    return (
        <div>
            <form onSubmit={onFormSubmit}>
                <div className="form">
                    <div className="form-group">
                        <label htmlFor="test1">test1</label>
                        <Field name="test1" component="input" type="text" />
                    </div>
                    <div className="form-group">
                        <label htmlFor="test2">test2</label>
                        <input name="test2" type="file" onChange={handleFiles} />
                    </div>
                    <div className="form-group">
                        <label htmlFor="test3">test3</label>
                        <input name="test3" type="file" onChange={handleFiles} />
                    </div>
                </div>
                <button type="submit">submit</button>
            </form>
        </div>
    )
}

const mapStateToProps = (state) => ({
    formDataState: state.getIn(['form', 'fileForm']),
    filesData: state.getIn(['files', 'files']),
});

const mapDispatchToProps = (dispatch) => ({
    onFile: (file, name) => dispatch(actions.files(file, name))
});

export default reduxForm({
    form: 'fileForm',
})(connect(mapStateToProps, mapDispatchToProps)(FileTest));
```
