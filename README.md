const PdpaConsent = () => import('@/projects/views/pdpa/index.vue')

//condition
const Cunion = () => import('@/projects/views/condition/con_union.vue')
const Cnormal = () => import('@/projects/views/condition/con_normal.vue')
const CSchool = () => import('@/projects/views/condition/con_school.vue')

//register
const Runion = () => import('@/projects/views/register/components/regis_union.vue')
const Rnormal = () => import('@/projects/views/register/components/regis_normal.vue')
const RSchool = () => import('@/projects/views/condition/con_school.vue')

// result score user
const Resultunion = () => import('@/projects/views/result/components/result_union.vue')
const Resultnormal = () => import('@/projects/views/result/components/result_normal.vue')
const ResultSchool = () => import('@/projects/views/result/components/result_school.vue')
const Resultasso = () => import('@/projects/views/result/components/result_assosiation.vue')

//ใส่ใน route /
{
          path: '/pdpa/:type',
          name: 'PdpaConsent',
          component: PdpaConsent
        }

//
{
      path: '/condition',
      name: 'condition',
      component: TheContainer_Landing,
      children: [
        {
          path: 'condition_union',
          name: 'Cunion',
          component: Cunion
        },
        {
          path: 'condition_normal',
          name: 'Cnormal',
          component: Cnormal
        },
        {
          path: 'condition_school',
          name: 'CSchool',
          component: CSchool
        },
      ]
    },

    {
      path: '/register',
      name: 'register',
      component: TheContainer_Landing,
      children: [
        {
          path: 'register_union',
          name: 'Runion',
          component: Runion
        },
        {
          path: 'register_normal',
          name: 'Rnormal',
          component: Rnormal
        },
        {
          path: 'register_school',
          name: 'RSchool',
          component: RSchool
        },
      ]
    },
    
{
      path: '/result',
      name: 'result',
      component: TheContainer_Landing,
      children: [
        {
          path: 'result_union',
          name: 'Resultunion',
          component: Resultunion
        },
        {
          path: 'result_normal',
          name: 'Resultnormal',
          component: Resultnormal
        },
        {
          path: 'result_school',
          name: 'ResultSchool',
          component: ResultSchool
        },
        {
          path: 'result_assosiation',
          name: 'Resultasso',
          component: Resultasso
        },
      ]
    },
